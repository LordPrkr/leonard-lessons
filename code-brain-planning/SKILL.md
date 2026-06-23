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

Write `plans/<00X_TOPIC>.md` with the goal, files to change, test strategy, verification commands, risks, links to scout artifacts, and links to any Code Brain ADRs. Use `obsidian_create_canvas` to sketch proposed behavior in `canvases/<TOPIC> Proposed.canvas` when comparing old vs new behavior would prevent rediscovery. Always create a Mermaid call-stack diagram in `diagrams/<TOPIC> Callstack.md`; add other Mermaid diagrams only when they clarify execution, state, or data flow.

Done when the plan is specific enough for another agent to implement without rediscovering the design, the call-stack diagram is linked, current/new behavior sketches are linked when created, and any resolved domain terms or decisions are linked from `domain/`.

### 3. Review

Get an adversarial review from an oracle/reviewer subagent when risk is meaningful; otherwise self-review against the plan.

Done when accepted feedback is edited into the plan and rejected feedback has a short reason.

### 4. Approval Gate

Present the plan and wait.

Done only when the user approves implementation or changes the plan.

### 5. Handoff

After approval, hand the approved plan to a worker with fresh context, explicit acceptance criteria, and verification commands.

Done when the fresh-context worker starts from the approved plan, not a new implicit one.
