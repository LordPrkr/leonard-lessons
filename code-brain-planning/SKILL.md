---
name: code-brain-planning
description: "Code Brain planning for broad, risky, cross-cutting, or approval-first code changes. Use when the user asks for Code Brain, durable planning artifacts, design review, scout/oracle review, or an implementation plan before coding."
---

# Code Brain Planning

Use this for durable planning, not ordinary edits. Store artifacts in `~/Documents/Code Brain/<project>/`, where `<project>` is the current repo/worktree name. Create the vault directory if missing.

## Steps

### 1. Scout

Inspect relevant code directly or with a scout subagent when the area is large.

Done when `canvases/<TOPIC>.canvas` or `notes/<TOPIC> Context.md` records the current setup and every likely touchpoint is named.

### 2. Plan

Write `plans/<00X_TOPIC>.md` with the goal, files to change, test strategy, verification commands, risks, and links to scout artifacts. Add Mermaid diagrams in `diagrams/` only when they clarify execution, state, or data flow.

Done when the plan is specific enough for another agent to implement without rediscovering the design.

### 3. Review

Get an adversarial review from an oracle/reviewer subagent when risk is meaningful; otherwise self-review against the plan.

Done when accepted feedback is edited into the plan and rejected feedback has a short reason.

### 4. Approval Gate

Present the plan and wait.

Done only when the user approves implementation or changes the plan.

### 5. Handoff

After approval, implement via `effective-engineer` or hand the approved plan to a worker with explicit acceptance criteria and verification commands.

Done when implementation starts from the approved plan, not a new implicit one.
