---
name: code-brain-planning
description: "Plan approval-first work in Code Brain, choosing a lightweight plan or managed lifecycle from the work's actual coordination needs."
---

# Code Brain Planning

Use this for implementation work that needs a durable, user-approved plan. Follow `/code-brain` for vault resolution, repository identity, vocabulary, and evidence; use `/code-brain-writeback` as findings emerge. Do not edit implementation files until the user explicitly approves the current plan.

Use `/code-brain-wayfinder` before planning when material decisions still obscure the implementation route. A clear route does not by itself require managed planning.

The parent owns plan metadata, `AGENTS.md`, and `KANBAN.md`; workers never change project navigation or workflow state. Code Brain artifacts are not source-repository commits.

## 1. Size the plan

Inspect the request and enough local context to choose the smallest durable shape:

- **Lightweight** — one bounded outcome fits one fresh worker; it needs an approval gate but no tracked handoff, formal receipt, execution slices, or coordination with another workstream.
- **Managed** — any of those needs is present, or the work is broad, risky, cross-cutting, or likely to outlive this session.
- **Wayfinding** — a material design, contract, ownership, security, or sequencing decision still prevents a responsible plan; hand off to `/code-brain-wayfinder`.

State the selected shape and why. If shape selection yields a material finding, stop and create the selected plan's draft `plan.md` before continuing reconnaissance so `/code-brain-writeback` has an activity artifact. For a lightweight plan, do not create a card, receipt, execution slices, or optional artifacts merely because managed planning supports them. For managed work, read [the managed lifecycle](./references/MANAGED-LIFECYCLE.md) before creating artifacts.

Done when the route is clear and the plan shape is justified by concrete coordination needs rather than the task's apparent importance, or the work has been handed to `/code-brain-wayfinder` because a material decision still blocks planning.

## 2. Create the plan

Ensure the Code Brain project is initialized; invoke `/code-brain` when `VISION.md` is absent. Scan `plans/`, create the next `plans/<NNN_TOPIC>/` folder, and read `/code-brain`'s plan authoring contract before writing `plan.md`. For Lightweight, use [the lightweight layout](./references/LIGHTWEIGHT.md); for Managed, read [`TEMPLATE.md`](./references/TEMPLATE.md).

Capture each affected source repository's full `HEAD`, then link every non-closed `plan.md` from `AGENTS.md` under Active plans. Write only the sections and sibling artifacts that the selected shape needs. Every created artifact has a relative link from `plan.md`. For managed work, create and link `notes.md` with `Exploration` and `Documentation candidates` sections before recording its first material finding. Lightweight plans use their layout's sections and omit `notes.md` unless exploration outgrows them.

Invoke supporting skills only for their concrete artifact or decision:

- `/domain-modeling` when the plan settles shared language, a bounded context, or an ADR-worthy decision.
- `/code-brain-diagramming` when a diagram makes a material flow, boundary, or choice easier to verify than prose.
- `/tracer-bullet` when runnable evidence is required to choose an implementation path.

For managed work, follow the lifecycle reference for the board card, review, slices, and receipt. Lightweight plans remain in `plans/` without a board card.

Done when `plan.md` stands alone for a fresh worker, every material claim has evidence or an explicit question, and no artifact exists without serving the selected plan shape.

## 3. Review and approve

Apply `/spellbinding-sentences` to the plan. Label every proposed diff and give it an explicit `WHY` tied to the observed behavior or requested outcome. Adversarially review meaningful risks; use a read-only second opinion for an irreversible migration, external contract, ownership or security boundary, unresolved architectural choice, or cross-repository coordination.

Incorporate accepted findings, then present the exact standalone plan and wait. Explicit approval sets `status: approved`; a substantive revision restores `draft` and repeats review. For managed work, use the lifecycle reference's board transition. An implemented plan is immutable; later work receives a new folder.

Done when the plan is approved and ready to execute, or its status honestly records abandonment or supersession.

## 4. Implement, verify, and close

Invoke `/feature-branch` before implementation. A lightweight plan is one fresh worker; managed work follows its execution slices. Give each worker only the approved `plan.md`, its assigned execution-slice identifier when applicable, and an instruction to invoke `/effective-engineer`; a managed worker implements only that slice. Review the delivered diff against the approved plan, repository standards, correctness, simplicity, and verification evidence. A design change requires a revised plan and approval.

Invoke `/finalize-implementation` for verified work. Record the outcome, changed files, verification, deviations, residual risks, and blockers in `plan.md` or `notes.md`; managed work also follows the receipt contract. Set `status: implemented` only after verified delivery and finalization succeed.

Done when every retained diff hunk is justified by the approved plan, delivery evidence is durable, and the plan status matches the result.
