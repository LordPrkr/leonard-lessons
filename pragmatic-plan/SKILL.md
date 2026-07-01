---
name: pragmatic-plan
description: "Pragmatic planning for lightweight approval-first code changes. Use when the user wants a standalone implementation plan before coding, especially with code snippets showing the intended end state."
---

# Pragmatic Plan

Use this for lightweight planning that must be approved before implementation. Do not edit implementation files while this skill is active unless the user explicitly approves the plan.

## Steps

### 1. Scout

Inspect relevant code directly. Use a scout subagent when the area is large or cross-cutting.

Done when every likely touchpoint is named and the current flow is understood well enough to avoid rediscovery during implementation.

### 2. Plan

Write a standalone plan for a worker with no prior knowledge. Include:

- goal and relevant context
- files to change
- TDD-first implementation steps
- important code snippets that show the intended end product, such as core business logic, database queries, API shapes, or component trees
- test strategy and verification commands
- risks or open questions

Do not mention prior plan versions, rejected directions, or how the plan changed.

Done when the plan can be handed to a fresh-context worker with no explanation, the TDD path is clear, and the snippets make the intended final shape concrete.

### 3. Approval Gate

Present the plan and wait. Do not implement it yet. If the user asks for changes, update the plan so it still stands on its own; do not mention prior plan versions, rejected directions, or how the plan changed.

Done only when the user approves implementation or asks for plan changes.
