---
name: code-brain-planning
description: "Code Brain planning for broad, risky, cross-cutting, or approval-first code changes. Use with /code-brain when the user asks for durable planning artifacts, design review, scout/oracle review, or an implementation plan before coding."
---

# Code Brain Planning

Use this for durable planning, not ordinary edits. Store artifacts using `/code-brain` project folder conventions. Create the vault directory if missing.

When planning sharpens domain language or records architectural decisions, invoke `domain-modeling`; its glossary and ADR source of truth is the Code Brain, not the repo.

## Plan Folder

Before writing artifacts, create the next numbered `plans/<00X_TOPIC>/` folder using `/code-brain` numbering. Keep all artifacts for that plan together:

```txt
plans/<00X_TOPIC>/
├── plan.md
├── notes.md
├── call-stack.diagram.md
├── current.canvas
└── proposed.canvas
```

Create optional artifacts only when useful. Give additional diagrams and canvases descriptive kebab-case names ending in `.diagram.md` and `.canvas`. In `plan.md`, link every created sibling with a relative Markdown link such as `[Context notes](./notes.md)`.

## Steps

Launch subagents asynchronously unless a foreground run is intentionally needed. Keep the parent session responsible for decisions, artifact persistence, and orchestration.

### 1. Build Context

Use a `scout` for bounded local codebase recon. For broad or cross-cutting work, use one or more fresh-context `context-builder` subagents with distinct scopes and output paths. Add a `researcher` only when external docs, recent changes, benchmarks, or primary sources materially affect the plan.

The parent persists useful findings in the plan folder's `notes.md` or a named `.canvas` sibling. Use `obsidian_create_canvas` when flow, state, ownership, or boundaries matter.

Done when the context artifact records the current setup, every likely touchpoint is named, external evidence is linked when relevant, and any domain-modeling questions are queued.

### 2. Challenge Direction

Use a forked `oracle` when inherited assumptions, architecture, scope, or trajectory need a second opinion. The oracle is advisory and must not edit code or planning artifacts. Skip it when the gathered context leaves no meaningful directional decision.

Done when the parent has accepted or rejected the oracle's recommendations before planning.

### 3. Plan

Give the gathered context and approved direction to a `planner`. The planner reads and produces a concrete implementation plan without editing project code. The parent then persists and refines the plan folder's `plan.md` as a standalone handoff artifact for a worker with no prior knowledge. Include:

- goal and relevant context
- files to change
- TDD-first implementation steps
- important new code snippets that show the intended end product, such as core business logic, database queries, API shapes, or component trees
- test strategy and verification commands
- risks
- questions for the user that must be answered before implementation
- links to context artifacts
- links to any Code Brain ADRs

Do not leave conditional forks in the worker plan. If the plan would say "if X, do Y; if not, do Z," stop and ask the user which branch to plan for instead.

Do not mention prior plan versions, rejected directions, or how the plan changed.

Use `obsidian_create_canvas` to sketch proposed behavior in `proposed.canvas`, with `current.canvas` when comparing old and new behavior would prevent rediscovery.

Always create a Mermaid call-stack diagram in `call-stack.diagram.md`; add other named `.diagram.md` siblings only when they clarify execution, state, or data flow.

Done when:

- the plan can be handed to a fresh-context worker with no explanation
- the TDD path is clear
- snippets make the intended final shape concrete
- every remaining branch is raised as a user question rather than embedded as an if/then instruction
- every created sibling artifact is linked with a relative path
- the call-stack diagram is linked
- current/new behavior sketches are linked when created
- any resolved domain terms or decisions are linked from `domain/`

### 4. Review the Plan

For meaningful risk, use a fresh-context `reviewer` to adversarially review the plan against the request and gathered evidence. The reviewer must inspect the artifacts directly and must not edit code or planning artifacts. Otherwise self-review.

Done when the parent edits accepted feedback into the plan with no revision-history residue, and records a short reason outside the plan for rejected feedback.

### 5. Approval Gate

Present the plan and wait. If the user asks for changes, update the plan so it still stands on its own; do not mention prior plan versions, rejected directions, or how the plan changed.

Done only when the user approves implementation or changes the plan.

### 6. Implement

After approval, launch a fresh-context `worker` asynchronously with the approved plan, explicit acceptance criteria, verification commands, and a required handoff covering changed files, commands and exit codes, validation evidence, residual risks, and decisions needing approval.

Done when the worker implements from the approved plan rather than inventing a new implicit one.

### 7. Review the Implementation

Launch fresh-context `reviewer` subagents with distinct, read-only angles such as correctness, validation, and simplicity. The parent synthesizes their findings. If fixes are worth doing now, launch one forked `worker` asynchronously to apply only the accepted fixes; review again when those fixes are substantial.

Done when no blocker or approved fix remains, focused verification passes, and the parent has inspected the final diff.

### 8. Commit

After the worker finishes and verification passes, invoke
`/conventional-commit-message`, then commit the implementation and related Code
Brain artifact updates with the generated Conventional Commit message.

Done when `git status` shows no uncommitted changes from the implementation or
Code Brain artifact updates.
