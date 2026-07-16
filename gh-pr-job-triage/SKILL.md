---
name: gh-pr-job-triage
description: Triage GitHub pull-request jobs with parallel scouts. Use when PR checks fail or the user wants CI failures classified as flaky, unrelated, or related to the changes.
---

# GitHub PR Job Triage

Delegate evidence collection; keep classification with the orchestrator.

## 1. Establish scope

Use `gh` to identify the current branch's pull request, immutable head SHA, base branch, changed files, and check runs. Classify only terminal failing conclusions; report queued, in-progress, cancelled, and skipped checks separately unless the user asks to triage them.

If there is no linked pull request, stop and report that. If every relevant terminal check passed, report that no triage is needed.

**Complete when:** every relevant terminal failure has its name, conclusion, details URL, and run/job identifier when available.

## 2. Discover scouts

Call `subagent({ action: "list" })`. Select an executable `scout`; stop and report the discovery failure if none is available.

**Complete when:** the scout runtime name is verified.

## 3. Fan out evidence collection

Launch one read-only scout per job in a single parallel `subagent` call with `context: "fresh"`, `async: true`, and bounded concurrency. Scouts must not edit files or launch subagents.

Give each scout the repository, PR number, head SHA, job name, details URL, and identifiers. Require it to use `gh` to inspect the check, workflow run, job metadata, annotations, and logs, then attempt the smallest safe reproduction when one is available. It may inspect the PR diff and nearby repository code only to connect log evidence to changed files.

Each scout returns:

```text
Job: <name>
Conclusion: <conclusion>
Failure: <exact failing command, test, or step>
Evidence: <short quoted log/annotation excerpts with URLs or run/job ids>
Change overlap: <changed files/symbols plausibly connected, or none>
History: <rerun/previous-run evidence of intermittence, or unknown>
Reproduction: <smallest safe command and result, or infeasible reason>
Missing evidence: <anything gh could not retrieve>
```

Scouts collect evidence only. They must not classify the job as flaky, unrelated, or related.

Use this execution shape, replacing placeholders and creating one task per job:

```typescript
subagent({
  tasks: [
    {
      agent: "<scout>",
      task: "Collect evidence for GitHub PR <pr> job <job>. Repository: <repo>. Head SHA: <sha>. Details: <url>. Use gh to inspect metadata, annotations, and logs. Inspect the diff only for change overlap. Do not classify or modify files. Return the required evidence format."
    }
  ],
  context: "fresh",
  concurrency: Math.min(<job-count>, 5),
  async: true
})
```

**Complete when:** one scout is running for every relevant job.

## 4. Classify from evidence

Continue any useful local inspection, then call `wait({ all: true })` when no independent work remains. Inspect failed scouts with `subagent({ action: "status", id: "..." })`; never infer a classification from a missing report.

The orchestrator—not the scouts—assigns exactly one classification:

- **Flaky:** evidence shows the same code and inputs can pass without a relevant change, or the failure is explicitly intermittent. A hunch, timeout, or successful rerun alone is insufficient without supporting history or a known flaky signature.
- **Unrelated:** the failure has no plausible dependency on the diff and evidence identifies an external, infrastructure, base-branch, or pre-existing cause.
- **Related:** the failing path overlaps changed behavior or dependencies and the evidence provides a credible causal link.
- **Inconclusive:** evidence cannot safely support any classification above. Request the smallest next action, such as rerunning one job or retrieving unavailable logs.

For each job, report the classification, confidence, decisive evidence, reproduction result, and next action. Separate facts from inference and link the run or job. For a related failure, the next action must name focused validation, repository-prescribed broader checks, and `/parallel-pr-review` after a fix.

**Complete when:** every scoped job is classified or explicitly marked inconclusive, and every classification cites decisive evidence.
