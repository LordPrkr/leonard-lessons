---
name: code-brain-slicing
description: "Define scoped tracker projects and delivery stories with acceptance criteria, tasks, and dependencies from settled goals, specifications, or wayfinding maps."
---

# Code Brain Slicing

Follow `$code-brain` for project conventions and the confirmed tracker workflow. When one bounded slice already exists and needs no project setup, hand it straight to `$code-brain-planning`.

## 1. Scope

Read the goal, specification, or wayfinding map and the relevant source, then agree the destination, inclusions, and exclusions with the user. Find an existing tracker project for this effort before proposing a new one.

Done when scope, exclusions, the target tracker project, and any unresolved decisions are explicit.

## 2. Draft

Draft a project brief and stories using [the formats](./references/FORMATS.md), each story an independently verifiable outcome sized for one plan. Give every story observable acceptance criteria, tasks, and only genuine blocking dependencies.

Done when every in-scope outcome is a story or an explicit deferral and the dependency graph is acyclic.

## 3. Confirm

Present the brief, stories, dependencies, and recommended first slice, and get explicit approval before changing the tracker. This approval covers the backlog only; each slice still needs plan approval.

Done when the user approves the project and backlog together.

## 4. Publish

Create or reuse the tracker project and one issue per story, then add dependency links once issue IDs exist. Record the project and story links in a slice index at `wayfinding/<NNN_TOPIC>/slices.md` (or `notes/<topic>-slices.md` without a map) and link it from the map or `AGENTS.md`.

Done when every approved story is published with verified project membership and the index path is reported.

## 5. Offer dispatch

List the ready stories and ask "Are you ready to dispatch these slices to T3 Code threads for implementation planning?" unless the user already requested dispatch. On yes, invoke `$code-brain-dispatch` with the slice index and tracker project; otherwise stop with those references.

Done when dispatch has started, or the user deferred it and the next action is clear.
