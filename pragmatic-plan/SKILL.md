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
- risks
- questions for the user that must be answered before implementation

Do not leave conditional forks in the worker plan. If the plan would say "if X, do Y; if not, do Z," stop and ask the user which branch to plan for instead.

Do not mention prior plan versions, rejected directions, or how the plan changed.

Done when the plan can be handed to a fresh-context worker with no explanation, the TDD path is clear, snippets make the intended final shape concrete, and every remaining branch is raised as a user question rather than embedded as an if/then instruction.

### 3. Approval Gate

Present the plan and wait. Do not implement it yet. If the user asks for changes, update the plan so it still stands on its own; do not mention prior plan versions, rejected directions, or how the plan changed.

Done only when the user approves implementation or asks for plan changes.

### 4. Implement

After approval, implement the approved plan and run its verification commands.

Done when the implementation matches the approved plan and every planned
verification command passes, or a failing command is reported with the smallest
useful failure detail.

### 5. Commit

Invoke `/conventional-commit-message`, then commit the verified implementation
with the generated Conventional Commit message.

Done when `git status` shows no uncommitted changes from the implementation.
