---
name: code-brain-slicing
description: "Turn a settled goal, specification, or wayfinding map into delivery stories with acceptance criteria, tasks, and dependencies when the work needs multiple implementation plans."
---

# Code Brain Slicing

Define the delivery backlog before planning individual slices. When a clear, bounded slice already exists, return it as input to `$code-brain-planning` without further decomposition. This skill produces agreed stories; detailed implementation design and plan approval belong to that planning workflow.

Use `$code-brain` for project identity, initialization, tracker setup, and evidence conventions. Read the project's `VISION.md`, relevant domain context and ADRs, and `ISSUE_TRACKER.md`. Follow its confirmed workflow for all tracker operations; complete missing setup before publishing.

## 1. Establish the scope

Read the supplied goal, specification, or wayfinding map, including relevant decision tickets and existing delivery issues. Inspect current source where needed to establish what already works and what remains to deliver.

Establish the destination and scope with the user from that evidence. Derive outcomes from the goal and requirements, using decisions as constraints shared by any relevant stories. Surface newly exposed product decisions to the user or the existing map, and settle them before treating affected stories as ready.

Done when the destination, in-scope outcomes, exclusions, existing work, and supporting sources are explicit, and unresolved decisions are identified.

## 2. Draft delivery stories

Read [story and index formats](./references/FORMATS.md) before writing stories or their index.

Split the scope into bounded, independently verifiable outcomes, each small enough for one implementation plan. Prefer slices that deliver a complete behavior across the required layers. Use real user stories for product behavior and verifiable technical outcomes for infrastructure work.

Give every story observable acceptance criteria covering success and material failure cases, delivery tasks, genuine blocking dependencies, and links to its requirements and decision evidence.

Done when every scoped outcome is covered by a story or an explicit proposed deferral, each story has checkable completion conditions and contributing tasks, dependencies have no cycles, and the first candidate slice or its blocking prerequisites are explicit.

## 3. Confirm the breakdown

Present the complete proposed stories, acceptance criteria, tasks, dependencies, deferrals, and recommended first slice or blockers. Resolve questions about scope, granularity, and ordering with the user, then obtain explicit approval before publishing or changing tracker issues.

Story approval authorizes the agreed backlog. Implementation still requires the separate plan review and approval in `$code-brain-planning`.

Done when the user has approved the breakdown and initial ordering, every exclusion or deferral is explicit, and all remaining blockers are recorded against the affected stories.

## 4. Publish and return the first slice

Find or create one delivery issue per approved story, reusing an issue for the same outcome and preserving unrelated issue content. Keep decision tickets as decision records and link them as evidence. Publish story content using the agreed format and confirmed tracker conventions; represent tasks within the story or as linked issues according to that workflow. Create or update dependency relationships after the required issue identifiers exist. The tracker owns story content, task status, and dependencies.

Create or update a compact slice index at `wayfinding/<NNN_TOPIC>/slices.md` when a map exists, otherwise `notes/<topic>-slices.md`. Link it from the map's Outcome or, without a map, the project's `AGENTS.md`. Preserve existing plan links. The index links to canonical issues and sources; it holds no copied story bodies or workflow status.

Check the current tracker state and return the first unblocked, available story and the index path as inputs for `$code-brain-planning`. If no story is available, report the blockers and leave planning pending.

Done when approved stories are published with their dependencies and evidence, the discoverable index and its absolute path have been reported, and the next slice is ready for planning or its blockers are explicit. Planning and implementation have not started as part of slicing.
