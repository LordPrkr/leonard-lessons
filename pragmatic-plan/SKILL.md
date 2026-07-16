---
name: pragmatic-plan
description: "Lightweight in-session planning with no Code Brain artifacts. Use when the user wants a concrete plan and approval loop for a bounded change that need not persist across sessions."
---

# Pragmatic Plan

Use this for lightweight planning held in the current session. Do not create Code Brain artifacts; use `code-brain-planning` when durable plans, board state, receipts, or cross-session execution are required. Do not edit implementation files until the user explicitly approves the current plan.

## Steps

### 1. Scout

Inspect the relevant code directly. Use bounded reconnaissance only when the area is large or cross-cutting.

Done when every likely touchpoint and the current flow are understood.

### 2. Plan and review

Write a standalone plan for a worker with no prior context. Include goal, relevant context, exact files, the highest existing public test seam, one red-green step per observable behavior, important end-state snippets, tests, verification commands, risks, and blocking questions. Do not leave conditional implementation branches or revision-history residue.

Adversarially self-review meaningful risk. Incorporate accepted findings into the standalone plan.

Done when the plan is concrete, executable, and ready for a user decision.

### 3. Approval gate

Present the plan and wait. Explicit approval applies only to the presented version. A substantive revision loops back through plan review and this approval gate; a change request is not approval.

Done when the user explicitly approves the current plan or ends the work.

### 4. Implement and verify

Implement only the approved plan and run its verification commands. Review the final diff against the approved plan, repository standards, correctness, and simplicity; re-run affected checks after fixes. A design change requires a revised plan and approval.

Done when implementation matches the plan, every retained diff hunk is justified by it, and verification passes, or the smallest useful failure detail and remaining risk are reported.

Do not commit automatically. Commit only when the user separately authorizes it.
