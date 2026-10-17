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

Invoke `$follow-precedent` to establish applicable patterns and `$spellbinding-sentences` for the plan's prose.

Ensure the Code Brain project is initialized; invoke `$code-brain` when `VISION.md` is absent. Scan `plans/`, create the next `plans/<NNN_TOPIC>/` folder, and read `$code-brain`'s plan authoring contract before writing `plan.md`. Use [the plan template](./references/TEMPLATE.md). Keep each plan small enough for one implementation subagent; split larger work into separate plans before approval.

Summarize applicable precedent using the shared authoring contract. In `Deviations`, record necessary departures and their authorization or the decision requested, including search gaps and conflicting examples.

Done when `plan.md` stands alone for a fresh implementation subagent, summarizes applicable precedent and necessary deviations, identifies unanswered questions, and fits one implementation subagent.

## 3. Review

Always spawn a read-only reviewer subagent to adversarially review the plan. Give it the standalone plan and source repository locations. Instruct it to look for security concerns, invoke `$follow-precedent` to identify deviations from repository style and precedent, and confirm that an agent with no prior knowledge can understand and implement the plan.

Incorporate accepted findings into the plan.

Done when the reviewer has returned its findings and accepted findings are reflected in the plan.

## 4. Approval

Resolve Questions with the user and record their answers following the shared contract. Present the exact standalone plan, including its deviations and their consequences, and wait for explicit approval. Approval covers disclosed departures only. Explicit approval sets `status: approved`; a substantive revision restores `draft` and repeats review. Remove abandoned or superseded plans from Active plans. An implemented plan is immutable; later work receives a new folder.

Done when the plan is approved with every departure explicitly authorized and no unresolved precedent conflict, or its status honestly records abandonment or supersession.

## 5. Implement

Delegate implementation to a worker subagent with the approved plan and an instruction to invoke `$effective-engineer`.

Done when the worker returns the finalized pull request and verification results, or reports its blockers.

## 6. Verify

Delegate review to a reviewer subagent with the delivered pull request or committed branch comparison, the approved plan as its spec, and an instruction to invoke `$code-review`.

Done when review is complete and actionable findings are resolved, or remaining blockers are reported.

## 7. Close

Create `receipt.md` using [the receipt format](./references/RECEIPT.md) and link it from Outcome. Set `status: implemented` and remove the plan from Active plans only after verified delivery, finalization, and the receipt are complete. Blocked or partial work remains `approved`; report its blockers in chat.

Done when the receipt links the finalized PR and records the review outcome and follow-up, and the plan status matches the result.
