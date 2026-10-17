---
name: code-brain-planning
description: "Create a durable, user-approved implementation plan in Code Brain, grounded in applicable repository precedent."
---

# Code Brain Planning

Use this for implementation work that needs a durable, user-approved plan. Complete step 1 before reconnaissance, wayfinding, or invoking supporting skills. Follow `/code-brain` for vault resolution, repository identity, vocabulary, and evidence. Do not edit implementation files until the user explicitly approves the current plan.

**Follow precedent.** After step 1 and before reconnaissance, invoke `/follow-precedent`. The plan must identify the patterns it reuses and disclose every necessary departure before approval.

Use `/code-brain-wayfinder` before planning when material decisions still obscure the implementation route.

The parent agent owns plan metadata, `AGENTS.md`, and the receipt; implementation subagents never change project navigation or plan status. Code Brain artifacts are not source-repository commits.

## 1. Update the planning checkout

For each affected source repository, use a clean `main` checkout and run `git pull --ff-only origin main` before inspecting source code or drafting the plan. Preserve existing work by using a separate worktree when the caller's checkout has local changes or is on a feature branch. If the pull fails or local `main` has diverged, resolve the checkout state and repeat the pull before planning.

Done when every planning checkout has a clean working tree and `HEAD` equals the freshly fetched `origin/main` commit.

## 2. Create the plan from precedent

Ensure the Code Brain project is initialized; invoke `/code-brain` when `VISION.md` is absent. Scan `plans/`, create the next `plans/<NNN_TOPIC>/` folder, and read `/code-brain`'s plan authoring contract before writing `plan.md`. Use [the plan template](./references/TEMPLATE.md). Keep each plan small enough for one implementation subagent; split larger work into separate plans before approval.

Capture each affected source repository's full `HEAD` in its Precedent citations, then link every non-closed `plan.md` from `AGENTS.md` under Active plans. Use the shared contract's concise sections, file tree, definition overview, and test strategy. Link supporting artifacts from the relevant plan section when needed.

Before drafting the definition overview, establish applicable precedent from the planning checkout. In `Precedent`, map each substantive implementation, validation, and testing choice to paths and symbols with the source revision and why the example applies. In `Deviations`, record each departure using the shared contract's disclosure fields and identify existing authorization or the decision requested. Record search gaps and conflicting examples explicitly. Carry these references into the definition overview and test strategy so a fresh implementation subagent can adapt the same patterns.

Invoke supporting skills only for their concrete artifact or decision:

- `/domain-modeling` when the plan settles shared language, a bounded context, or an ADR-worthy decision.
- `/code-brain-diagramming` when a diagram makes a material flow, boundary, or choice easier to verify than prose.
- `/tracer-bullet` when runnable evidence is required to choose an implementation path.

Done when `plan.md` stands alone for a fresh implementation subagent, every substantive choice maps to applicable precedent or a disclosed necessary deviation, every material claim has evidence or an explicit question, and the plan fits one implementation subagent.

## 3. Review and approve

Apply `/spellbinding-sentences` to the plan and check it against the shared authoring contract. Audit the definition overview and test strategy against `Precedent` and `Deviations`; remove departures without demonstrated necessity. Adversarially review meaningful risks; use a second opinion from a read-only reviewer subagent for an irreversible migration, external contract, ownership or security boundary, unresolved architectural choice, or cross-repository coordination.

Update Questions as answers arrive in chat, following the shared contract. Incorporate accepted findings, then present the exact standalone plan, including its deviations and their consequences, and wait. Approval covers disclosed departures only. Explicit approval sets `status: approved`; a substantive revision restores `draft` and repeats review. Remove abandoned or superseded plans from Active plans. An implemented plan is immutable; later work receives a new folder.

Done when the plan is approved with every departure explicitly authorized and no unresolved precedent conflict, or its status honestly records abandonment or supersession.

## 4. Implement, verify, and close

Code Brain owns delivery for its approved plans. Invoke `/feature-branch` once before implementation to establish the feature branch and independently provisioned worktree. Spawn an implementation subagent with fresh context for the whole plan. Give it only the approved `plan.md` and an instruction to invoke `/effective-engineer`; state that Code Brain owns workspace provisioning, finalization, the receipt, and plan closure. The subagent returns its diff, verification results, deviations, and blockers. Review the delivered diff against the approved plan, its cited precedent and authorized deviations, repository standards, correctness, simplicity, and verification results. A design change requires a revised plan and approval.

Invoke `/finalize-implementation` once for verified work. After finalization, create `receipt.md` using [the receipt format](./references/RECEIPT.md) and link it from Outcome. Set `status: implemented` and remove the plan from Active plans only after verified delivery, finalization, and the receipt are complete. Blocked or partial work remains `approved`; report its blockers in chat.

Done when every retained diff hunk follows the approved plan and its cited precedent or authorized deviations, the receipt links the finalized PR, and the plan status matches the result.
