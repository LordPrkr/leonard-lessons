---
name: pragmatic-plan
description: "Lightweight planning with immediate Code Brain writeback. Use when the user wants a concrete plan and approval loop for a bounded change without a managed planning lifecycle."
---

# Pragmatic Plan

Use this for lightweight planning with one durable field note. Follow `/code-brain` for vault resolution, repository identity, and evidence, and `/code-brain-writeback` while producing the note. Use `code-brain-planning` when board state, formal receipts, execution slices, or cross-session orchestration are required. Do not edit implementation files until the user explicitly approves the current plan.

Keep the field note at `notes/plans/YYYY-MM-DD-<topic>.md` with four sections: `Exploration`, `Documentation candidates`, `Plan`, and `Outcome`.

## Steps

### 1. Scout

Inspect the relevant code directly. Use bounded reconnaissance only when the area is large or cross-cutting.

Apply `/code-brain-writeback` with findings under `Exploration` and reusable-candidate pointers under `Documentation candidates`.

Done when every likely touchpoint and the current flow are understood, and every material finding is already present in the field note.

### 2. Plan and review

Apply `/code-brain`'s plan authoring contract and `/spellbinding-sentences` to the plan's prose. Adversarially self-review meaningful risk, incorporate accepted findings into the standalone plan, and apply `/code-brain-writeback` to the reviewed `Plan` before presenting it.

Done when the field note contains the exact plan presented for approval, the plan satisfies `/code-brain`'s authoring contract, and it is ready for a user decision.

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
