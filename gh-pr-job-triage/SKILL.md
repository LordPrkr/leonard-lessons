---
name: gh-pr-job-triage
description: Triage failing GitHub pull-request checks with token-lean gh commands. Use when PR checks fail or the user wants CI failures classified as flaky, unrelated, or related to the changes.
---

# GitHub PR Job Triage

Read the smallest slice of each log that names the cause, never a whole log.

## 1. Scope

```sh
gh pr view --json number,headRefOid,baseRefName,files -q '{n:.number,sha:.headRefOid,base:.baseRefName,files:[.files[].path]}'
gh pr checks --json name,bucket,link,workflow \
  -q '.[]|select(.bucket=="fail")|{name,workflow,link,ids:(.link|capture("runs/(?<run>[0-9]+)/job/(?<job>[0-9]+)")?)}'
```

Stop if there is no PR or nothing failed. A check without `ids` runs outside GitHub Actions; triage it from its `link` with that provider's tooling.

**Complete when:** every failing check has its name, link, and run and job IDs or an external link.

## 2. Extract each failure

Annotations come first; test reporters often put `file:line` and the assertion there:

```sh
gh api "repos/{owner}/{repo}/check-runs/$JOB/annotations" -q '.[]|"\(.annotation_level) \(.path):\(.start_line) \(.message)"'
```

When they only say `Process completed with exit code N`, save the cleaned job log and print the failing step's command and output before each `##[error]`:

```sh
gh api --allow-escape-sequences "repos/{owner}/{repo}/actions/jobs/$JOB/logs" \
  | sed -E 's/^(\xEF\xBB\xBF)?[0-9T:.-]+Z //; s/\x1b\[[0-9;]*[A-Za-z]//g' > "/tmp/job-$JOB.log"
awk '/^##\[group\]/{cmd=$0; skip=1; out=""; next} /^##\[endgroup\]/{skip=0; next} skip{next}
     /^##\[error\]/{print cmd; printf "%s", out; print; print "--"; next} {out=out $0 "\n"}' "/tmp/job-$JOB.log" | tail -n 80
```

If the window is empty or cut off, for example because the step's output is grouped, search the saved log with `rg -n` for the runner's failure markers and read only the surrounding lines with `sed -n 'A,Bp'`. Prefer this endpoint to `gh run view --log-failed`, which prefixes every line with job and step names and can return the whole job when it cannot map steps. Logs exist only for completed jobs; wait on a running one with `gh run watch "$RUN" --compact --exit-status`.

With several failing jobs, extract them in parallel. Use read-only subagents if your harness has them.

**Complete when:** every failing job has a quoted excerpt naming the failing command, test, or step.

## 3. Gather history

```sh
gh run view "$RUN" --attempt 1 --json jobs -q '.jobs[]|select(.name=="<job name>")|.conclusion'
gh run list --workflow "<workflow>" --branch "<base>" -L 10 --json conclusion,headSha,createdAt \
  -q '.[]|"\(.conclusion) \(.headSha[:7]) \(.createdAt)"'
```

Earlier attempts on the same SHA show flakiness; base-branch failures show a pre-existing cause. Compare the excerpt with the PR's changed files. Rerun with `gh run rerun "$RUN" --job "$JOB"` only when the user asks.

**Complete when:** every job has its prior-attempt and base-branch evidence, or is marked unknown.

## 4. Classify

Label each job **Flaky** (shown to pass on the same inputs), **Unrelated** (external or pre-existing cause), **Related** (credible causal link to the diff), or **Inconclusive** (name the next action). For related failures, recommend focused checks and `$code-scry <base-branch>` after the fix.

**Complete when:** every job has a classification with its decisive excerpt and next action.
