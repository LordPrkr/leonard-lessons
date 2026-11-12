---
name: gh-pr-job-triage
description: Triage GitHub pull-request jobs with parallel scout subagents. Use when PR checks fail or the user wants CI failures classified as flaky, unrelated, or related to the changes.
---

# GitHub PR Job Triage

Scouts collect evidence; you classify.

## 1. Scope

Use `gh` to find the branch's PR, head SHA, base, changed files, and terminal failing checks, stopping if there is no PR or nothing failed.

**Complete when:** every failing check has its name, details URL, and run or job ID.

## 2. Fan out scouts

Find a `scout` with `subagent({ action: "list" })`, then launch one read-only scout per job in a single `subagent({ tasks, context: "fresh", async: true, concurrency: Math.min(jobs, 5) })` call. Each scout inspects the job's logs and annotations with `gh`, tries the smallest safe reproduction, and returns this report without classifying:

```text
Job / Conclusion / Failure: <failing command, test, or step>
Evidence: <quoted log excerpts with links>
Change overlap: <connected changed files, or none>
History: <rerun or prior-run evidence, or unknown>
Reproduction: <command and result, or why infeasible>
```

**Complete when:** one scout is running per failing job.

## 3. Classify

After `wait({ all: true })`, label each job **Flaky** (shown to pass on the same inputs), **Unrelated** (external or pre-existing cause), **Related** (credible causal link to the diff), or **Inconclusive** (name the next action). For related failures, recommend focused checks and `$code-scry <base-branch>` after the fix.

**Complete when:** every job has a classification with its decisive evidence and next action.
