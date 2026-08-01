---
name: pragmatic-plan
description: "Lightweight planning with immediate Code Brain writeback. Use when the user wants a concrete plan and approval loop for a bounded change without a managed planning lifecycle."
---

# Pragmatic Plan

Use this for lightweight planning with one durable field note. Follow `/code-brain` for vault resolution, repository identity, and evidence. Use `code-brain-planning` when board state, formal receipts, execution slices, or cross-session orchestration are required. Do not edit implementation files until the user explicitly approves the current plan.

Keep the field note at `notes/plans/YYYY-MM-DD-<topic>.md`. Create it on the first material finding, then maintain four sections: `Exploration`, `Documentation candidates`, `Plan`, and `Outcome`. A material finding affects scope or design, resolves uncertainty, or would be costly to rediscover; routine file listings and transient dead ends stay in the session.

## Steps

### 1. Scout

Inspect the relevant code directly. Use bounded reconnaissance only when the area is large or cross-cutting.

Immediately after establishing each material finding, persist it under `Exploration` with `/code-brain` evidence before making another exploratory tool call. When it is reusable beyond this change, also add one concise item under `Documentation candidates`; do not promote it during planning. Update an existing finding instead of duplicating it when later evidence sharpens or disproves it.

Done when every likely touchpoint and the current flow are understood, and every material finding is already present in the field note.

### 2. Plan and review

Write a standalone plan for a worker with no prior context. Include goal, relevant context, exact files, the highest existing public test seam, one red-green step per observable behavior, tests, verification commands, risks, and blocking questions. Do not leave conditional implementation branches or revision-history residue.

Every implementation step that adds, removes, or modifies code must name each affected repository-relative path and immediately show the relevant change as a fenced unified diff. The diff must include enough unchanged context and `-`/`+` lines to distinguish current code from proposed code; never present proposed code as an unmarked end-state snippet. Use `/dev/null` for a new or deleted file, and include the full contents of a small new file.

**`src/example.ts`**

```diff
-export const example = "current"
+export const example = "proposed"
```

Adversarially self-review meaningful risk. Incorporate accepted findings into the standalone plan. Write the reviewed plan under `Plan` before presenting it to the user; replace that section after substantive revisions rather than preserving revision residue.

Done when the field note contains the exact concrete, executable plan presented for approval, every code-changing step has path-labeled before/after diffs, and the plan is ready for a user decision.

### 3. Approval gate

Present the plan and wait. Explicit approval applies only to the presented version. A substantive revision loops back through plan review and this approval gate; a change request is not approval.

Done when the user explicitly approves the current plan or ends the work.

### 4. Choose the branch

Invoke `/feature-branch` with the approved plan before implementation.

Done when the work is assigned to the current feature branch.

### 5. Implement and verify

Spawn exactly one `worker` subagent with `context: "fresh"`. Its task contains the approved plan verbatim plus an instruction to invoke `/effective-engineer` before executing it; include no parent conversation or other implementation direction. The worker reports changed files, command exit codes, validation evidence, deviations, residual risks, and blockers.

Wait for the worker before reviewing the diff against the approved plan, repository standards, correctness, and simplicity. Re-run affected checks after accepted fixes. A design change requires a revised plan and approval.

Done when the worker report and final diff match the plan, every retained diff hunk is justified by it, and verification passes, or the smallest useful failure detail and remaining risk are reported.

### 6. Finalize implementation

Invoke `/finalize-implementation` for verified work. Record the resulting changed files, verification, pull request, Jira result, deviations, and residual risks under `Outcome`; record blockers honestly when finalization does not complete.

Done when finalization returns and the field note records its outcome or smallest useful blocker.
