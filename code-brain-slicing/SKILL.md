---
name: code-brain-slicing
description: "Define scoped tracker projects and delivery stories with acceptance criteria, tasks, and dependencies from settled goals, specifications, or wayfinding maps."
---

# Code Brain Slicing

Define a scoped delivery project and its backlog before planning individual slices. When a clear, bounded slice already exists and no project setup is needed, return it as input to `$code-brain-planning` without further decomposition. This skill produces an agreed project and stories; detailed implementation design and plan approval belong to that planning workflow.

Use `$code-brain` for project identity, initialization, tracker setup, and evidence conventions. Read the project's `VISION.md`, relevant domain context and ADRs, and `ISSUE_TRACKER.md`. Follow its confirmed workflow for all tracker operations; complete missing setup before publishing.

## 1. Establish the scope

Read the supplied goal, specification, or wayfinding map, including relevant decision tickets and existing delivery issues. Inspect current source where needed to establish what already works and what remains to deliver.

Establish the destination and scope with the user from that evidence. Derive outcomes from the goal and requirements, using decisions as constraints shared by any relevant stories. Surface newly exposed product decisions to the user or the existing map, and settle them before treating affected stories as ready.

Identify the effort's tracker grouping using the confirmed scoped-project rules. Inspect any project reference already supplied or recorded in its slice index, then look for an existing project matching the goal and scope. Propose reuse or creation within the allowed scope; complete missing project configuration through `$code-brain` before publication.

Done when the destination, in-scope outcomes, exclusions, existing work, supporting sources, and proposed tracker project are explicit, and unresolved decisions are identified.

## 2. Draft the project and stories

Read [project, story, and index formats](./references/FORMATS.md) before drafting the scoped project brief, stories, or their index.

Draft the project brief using that format.

Split the scope into bounded, independently verifiable outcomes, each small enough for one implementation plan. Prefer slices that deliver a complete behavior across the required layers. Use real user stories for product behavior and verifiable technical outcomes for infrastructure work.

Give every story observable acceptance criteria covering success and material failure cases, delivery tasks, genuine blocking dependencies, and links to its requirements and decision evidence.

Done when the project brief defines the effort's boundaries and completion conditions, every scoped outcome is covered by a story or an explicit proposed deferral, each story has checkable completion conditions and contributing tasks, dependencies have no cycles, and the first candidate slice or its blocking prerequisites are explicit.

## 3. Confirm the breakdown

Present the project brief, target tracker scope, proposed project reuse or creation, complete stories, acceptance criteria, tasks, dependencies, deferrals, and recommended first slice or blockers. Resolve questions about scope, granularity, and ordering with the user, then obtain explicit approval for the project and backlog together before creating or changing tracker projects or issues.

This approval authorizes the agreed project and backlog. Implementation still requires the separate plan review and approval in `$code-brain-planning`.

Done when the user has approved the project brief, tracker destination, reuse or creation, breakdown, and initial ordering, every exclusion or deferral is explicit, and all remaining blockers are recorded against the affected stories.

## 4. Publish and return the first slice

Recheck for the selected or matching scoped project before creating one, then reuse it or create the approved grouping through the configured workflow. Publish the approved brief in the project description or equivalent, preserving unrelated content, and retain its URL or stable ID. If project operations are unavailable, report the access or capability gap and keep publication pending.

As soon as the project reference is known, create or update a compact slice index at `wayfinding/<NNN_TOPIC>/slices.md` when a map exists, otherwise `notes/<topic>-slices.md`. Record the project reference there and link the index from the map's Outcome or, without a map, the project's `AGENTS.md`. Preserve existing plan links. The index links to canonical issues and sources; it holds no copied story bodies or workflow status.

Find or create one delivery issue per approved story, reusing an issue for the same outcome and preserving unrelated issue content. Associate each story with the scoped project and verify membership through the configured tracker workflow. Keep decision tickets as decision records and link them as evidence. Publish story content using the agreed format and confirmed tracker conventions; represent tasks within the story or as linked issues according to that workflow. Add story links to the index as publication succeeds, and create or update dependency relationships after the required issue identifiers exist. The tracker owns the project brief, story content, task status, and dependencies.

If publication is partial, report the retained project and issue references and remaining work, and leave planning pending.

Once publication is complete, check the current tracker state and return the first unblocked, available story and the index path as inputs for `$code-brain-planning`. If no story is available, report the blockers and leave planning pending.

Done when the approved project exists, every approved story is published in it with verified membership, dependencies, and evidence, the discoverable index records the project reference and its absolute path has been reported, and the next slice is ready for planning or its blockers are explicit. Planning and implementation have not started as part of slicing.
