---
name: effective-engineer
description: "Implement code changes through a tight inspect, test, implement, verify, and review loop. Use for direct changes or when another workflow delegates an approved plan."
---

# Effective Engineer

Use the tight loop. When executing an approved plan, treat it as the scope and implementation direction. Escalate unplanned broad, risky, or cross-cutting work to `code-brain-planning`.

## Steps

### 1. Inspect

Read the smallest set of files needed to understand the change.

Done when you can name the files/functions to change, or you have one focused clarification question that blocks work.

### 2. Invoke `/tdd`

For non-trivial logic, invoke `/tdd` at the highest existing public seam. For each observable behavior: write one test, confirm it fails for the intended reason, add the minimum green implementation, then repeat. Skip only for trivial wiring, docs, or mechanical edits.

Done when each intended behavior has gone red then green at a public seam, or the skip reason is explicit.

### 3. Implement

Make the smallest code change that satisfies the current red test. Do not add abstractions for future cases.

Done when the requested behavior is implemented with the shortest maintainable diff.

### 4. Verify

Run targeted checks first, then repository-mandated aggregate checks or the full suite when feasible and proportionate to the blast radius.

Done when required checks pass, or any remaining failure is unrelated and named.

### 5. Review

Review the final diff against the request, repository standards, correctness, and simplicity. Re-run affected checks after fixes.

Done when every retained change is justified by the request and no actionable review finding remains.

### 6. Summarize

Report changed files and verification.

Done when the user can see what changed and what was run.
