---
name: code-brain-planning
description: "Create a durable, user-approved implementation plan in Code Brain, grounded in applicable repository precedent."
---

# Code Brain Planning

Use this for implementation work that needs a durable, user-approved plan. Code Brain artifacts are not source-repository commits.

## 1. Update the planning checkout

- If the base is unspecified and cannot be inferred from the conversation, use a clean `main` checkout and run `git pull --ff-only origin main` before inspecting source code or drafting the plan.
- Otherwise, use the base established by the conversation, such as the current branch when planning work on top of it. Ensure the planning checkout reflects the latest version of that base before inspecting source code or drafting the plan.

Done when each affected repository's planning checkout reflects the latest version of the selected base, including a successful pull when defaulting to `main`.

## 2. Create the plan from precedent

Establish precedent from the closest existing implementations, callers, and tests with the same responsibility, trust boundary, and lifecycle. Invoke `$spellbinding-sentences` for the plan's prose.

Ensure the Code Brain project is initialized; invoke `$code-brain` when `VISION.md` is absent. Scan `plans/`, create the next `plans/<NNN_TOPIC>/` folder, and read `$code-brain`'s plan authoring contract before writing `plan.md`. Use [the plan template](./references/TEMPLATE.md). Keep each plan small enough for one implementation subagent; split larger work into separate plans before approval.

When planning a delivery story, read its full acceptance criteria and current dependencies. Link the story from Problem and make Goal cover every criterion. Link the resulting plan beside the story in its slice index when one exists.

Done when `plan.md` stands alone for a fresh implementation subagent, summarizes applicable precedent, lists the affected scope, and fits one implementation subagent.

## 3. Approval

Raise open questions, unresolved story prerequisites, and any necessary departure from precedent with the user, and reflect each answer in the plan. Present the exact standalone plan and wait for explicit approval. Explicit approval sets `status: approved`; a substantive revision restores `draft` and requires approval again. Remove abandoned or superseded plans from Active plans. An implemented plan is immutable; later work receives a new folder.

Done when the plan is approved with every question resolved and every departure explicitly authorized, or its status honestly records abandonment or supersession.

## 4. Implement

Delegate implementation to a worker subagent with the approved plan and an instruction to invoke `$effective-engineer`.

Done when the worker returns the finalized pull request and verification results, or reports its blockers.

## 5. Verify

Delegate review to a reviewer subagent with the delivered pull request or committed branch comparison, the approved plan as its spec, and an instruction to invoke `$code-scry`.

Done when review is complete and actionable findings are resolved, or remaining blockers are reported.

## 6. Close

Create `receipt.md` using [the receipt format](./references/RECEIPT.md) and link it from Outcome. Set `status: implemented` and remove the plan from Active plans only after verified delivery, finalization, and the receipt are complete. Blocked or partial work remains `approved`; report its blockers in chat.

Done when the receipt links the finalized PR and records the review outcome and follow-up, and the plan status matches the result.
