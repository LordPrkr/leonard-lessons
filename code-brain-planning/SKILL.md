---
name: code-brain-planning
description: "Create a durable, user-approved implementation plan in Code Brain, grounded in applicable repository precedent."
---

# Code Brain Planning

Follow `$code-brain` for project conventions, initializing it first when `VISION.md` is missing.

## 1. Update the base

Check out the base established in the conversation, or a clean `main` after `git pull --ff-only origin main`, and pull it current.

Done when the planning checkout matches the latest base.

## 2. Draft the plan

Write `plans/<NNN_TOPIC>/plan.md` from [the template](./references/TEMPLATE.md) with `$spellbinding-sentences`, grounding Precedent in the closest existing implementations and tests. For a delivery story, link the issue from Problem, cover every acceptance criterion in Goal, and link the plan from its slice index.

Done when a fresh subagent could implement `plan.md` without this conversation, and it fits one subagent (split it otherwise).

## 3. Approve

Resolve open questions and departures from precedent with the user, then set `status: approved` only on their explicit approval. A substantive revision returns the plan to `draft`.

Done when the plan is `approved`, or marked `abandoned` or `superseded` and removed from Active plans.

## 4. Implement and review

Delegate the approved plan to a worker subagent running `$effective-engineer`, then delegate the delivered PR to a separate reviewer subagent running `$code-scry` with the plan as its spec.

Done when the PR is finalized and actionable review findings are resolved, or blockers are reported.

## 5. Close

Write `receipt.md` beside the plan with Delivery (PR link), Review (findings and resolution), and Follow-up sections, link it from Outcome, set `status: implemented`, and remove the plan from Active plans. Leave blocked or partial work `approved`, and treat an `implemented` plan as immutable.

Done when the receipt exists and the plan status matches the delivered result.
