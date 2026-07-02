---
name: code-brain-planning
description: "Code Brain planning for broad, risky, cross-cutting, or approval-first code changes. Use with /code-brain when the user asks for durable planning artifacts, design review, scout/oracle review, or an implementation plan before coding."
---

# Code Brain Planning

Use this for durable planning, not ordinary edits. Store artifacts using `/code-brain` project folder conventions. Create the vault directory if missing.

When planning sharpens domain language or records architectural decisions, invoke `domain-modeling`; its glossary and ADR source of truth is the Code Brain, not the repo.

## Steps

### 1. Scout

Inspect relevant code directly or with a scout subagent when the area is large. Use `obsidian_create_canvas` to sketch current behavior in `canvases/<TOPIC>.canvas` when flow, state, ownership, or boundaries matter.

Done when `canvases/<TOPIC>.canvas` or `notes/<TOPIC> Context.md` records the current setup, every likely touchpoint is named, and any domain-modeling questions are queued.

### 2. Plan

Write `plans/<00X_TOPIC>.md` as a standalone handoff artifact for a worker with no prior knowledge. Include:

- goal and relevant context
- files to change
- TDD-first implementation steps
- important new code snippets that show the intended end product, such as core business logic, database queries, API shapes, or component trees
- test strategy and verification commands
- risks
- questions for the user that must be answered before implementation
- links to scout artifacts
- links to any Code Brain ADRs

Do not leave conditional forks in the worker plan. If the plan would say "if X, do Y; if not, do Z," stop and ask the user which branch to plan for instead.

Do not mention prior plan versions, rejected directions, or how the plan changed.

Use `obsidian_create_canvas` to sketch proposed behavior in `canvases/<TOPIC> Proposed.canvas` when comparing old vs new behavior would prevent rediscovery.

Always create a Mermaid call-stack diagram in `diagrams/<TOPIC> Callstack.md`; add other Mermaid diagrams only when they clarify execution, state, or data flow.

Done when:

- the plan can be handed to a fresh-context worker with no explanation
- the TDD path is clear
- snippets make the intended final shape concrete
- every remaining branch is raised as a user question rather than embedded as an if/then instruction
- the call-stack diagram is linked
- current/new behavior sketches are linked when created
- any resolved domain terms or decisions are linked from `domain/`

### 3. Review

Get an adversarial review from an oracle/reviewer subagent when risk is meaningful; otherwise self-review against the plan.

Done when accepted feedback is edited into the plan with no revision-history residue, and rejected feedback has a short reason outside the plan.

### 4. Approval Gate

Present the plan and wait. If the user asks for changes, update the plan so it still stands on its own; do not mention prior plan versions, rejected directions, or how the plan changed.

Done only when the user approves implementation or changes the plan.

### 5. Handoff

After approval, hand the approved plan to a worker with fresh context, explicit acceptance criteria, and verification commands.

Done when the fresh-context worker starts from the approved plan, not a new implicit one.
