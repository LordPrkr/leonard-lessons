---
name: effective-engineer
description: "Project-agnostic skill for implementing features and documenting changes. Use when making any substantial code change."
---

# Effective Engineering

## Your Task

Design a plan and implement a feature using Test-Driven Development (TDD). Prefer the simplest solution that satisfies the request. During planning, maintain a "Code Brain" wiki about the current project in `~/Documents/Code Brain`. Each step produces an explicit artifact; do not move on until that artifact exists.

## Code Brain

Use the current repo/worktree to choose `<project>`. Store planning artifacts in the Code Brain Obsidian vault at `~/Documents/Code Brain/<project>/`. If `~/Documents/Code Brain` does not exist yet, create it as an Obsidian vault before writing artifacts.

## Steps

### 1. Gather Context

Spawn a scout subagent to understand the relevant code, then ask clarification questions.

Artifact: write a summary of the relevant code and an Obsidian Canvas describing how things are currently set up to `~/Documents/Code Brain/<project>/canvases/`.

### 2. Write the Plan

Create an implementation plan. Write it into the Code Brain Obsidian vault, under the matching project folder: `~/Documents/Code Brain/<project>/plans/<00X_PLAN_NAME>.md`. Link the plan to the scout's canvas from step 1.

Create any helpful Mermaid diagrams for the plan in `~/Documents/Code Brain/<project>/diagrams/<DIAGRAM_NAME>.md`, then link them from the plan with an Obsidian wikilink. Prefer diagrams that explain execution, not decoration: call stacks, sequence diagrams, state machines, or data-flow diagrams. Skip diagrams if the change is too small to need one.

Artifact: the implementation plan plus any created Mermaid diagrams, 0-n diagrams depending on complexity.

### 3. Review the Plan

Ask an oracle/reviewer subagent for an adversarial review of the plan. Edit the plan to account for useful feedback.

Artifact: the updated plan.

### 4. Get Approval

Present the plan to the user. Do **not** proceed until the user approves it.

Artifact: the user's approval.

### 5. Implement with TDD

Have a worker subagent implement the approved plan using TDD.

Artifact: updated code with tests.

### 6. Verify the Diff

Run the smallest relevant verification set on the diff: typecheck, lint, and tests where available. If static analysis or tests find lingering issues, return to step 5 and fix them.

Artifact: static analysis and test output.

### 7. Review the Diff

Run parallel reviewers on the diff: correctness, tests, and unnecessary complexity. For React changes, also review React performance and composition patterns. For major outstanding issues, return to step 5 and fix them. If implementation reveals problems with the approved plan, ask the user clarifying questions before continuing.

Artifact: a thorough code review.
