---
name: code-brain-wayfinder
description: "Chart and resolve an uncertain, multi-session effort as decision tickets in the project's configured issue tracker."
disable-model-invocation: true
---

# Code Brain Wayfinder

Use this before `$code-brain-planning` when the destination is clear but the route is not: the work has material decisions that cannot responsibly become one implementation plan yet. It is a decision workflow, not feature delivery.

Use the repository identity, issue-tracker setup, and evidence conventions from `$code-brain`. Read the project's `ISSUE_TRACKER.md` and follow its confirmed workflow for tracker operations. Complete setup before tracker operations when that configuration is missing or incomplete. Ticket notes hold questions, evidence, and resolutions; their linked issues hold workflow status.

Read [map and ticket formats](./references/FORMATS.md) before creating or changing a map or ticket.

## Terms

- **Map:** one `wayfinding/<NNN_TOPIC>/map.md` file that names the destination and indexes resolved decisions.
- **Ticket:** one note under its map's `tickets/` directory linked to one issue in the configured tracker; it resolves one focused decision or directly unblocks one, sized to one agent session. Split questions that exceed that bound into linked tickets with explicit dependencies, including when their scope grows during investigation.
- **Frontier:** unresolved, unblocked tickets available to work under the confirmed tracker workflow.
- **Fog:** in-scope uncertainty that cannot yet be stated as a ticket question.

## 1. Chart the map

1. Read the relevant Code Brain context, ADRs, source evidence, and existing issues in the configured tracker.
2. Establish the destination with the user. It must say what becomes possible when wayfinding ends, not how to build it.
3. Explore breadth-first, separating facts discoverable from source or research from decisions that require the user.
4. Create the numbered map and only the ticket notes whose questions are precise now. Record the remaining in-scope uncertainty as fog and explicit exclusions as out of scope.
5. Find or create one issue for every ticket, reusing an existing issue for the same question. Record its URL or stable ID in the ticket note. Represent availability and known blockers using the confirmed tracker workflow.

Done when the destination, initial frontier, known blockers, fog, and out-of-scope boundary are explicit; every ticket references exactly one issue; and no feature implementation has started.

## 2. Work one ticket

1. Read the map and current tracker state, then select the named frontier ticket or the next available ticket using the configured ordering. Claim its issue through the confirmed workflow before investigating.
2. Resolve according to type:
   - **Grilling:** ask the user one decision at a time. Do not answer on their behalf.
   - **Research:** use primary sources and record cited findings in the ticket note.
   - **Prototype:** follow the [prototype workflow](./references/PROTOTYPES.md) for an experiment or a discussion that requires human feedback.
   - **Task:** perform only the narrow manual work needed to unblock a decision.
3. Record the answer, evidence, and consequences in the ticket note. Add a one-line linked gist to the map's Decisions section.
4. Resolve the issue through the confirmed workflow. Promote newly precise fog into ticket notes and linked issues; update or close issues invalidated by the decision, distinguishing cancellation from resolution according to tracker conventions.

Done when the selected ticket has a durable resolution, every material claim has evidence, its issue is resolved, and tracker availability and dependencies reflect the newly known route.

## 3. Hand off to a new session

Check the current tracker state for every ticket. Proceed when every in-scope ticket is resolved or explicitly cancelled and no material fog remains. Blocked tickets and tickets claimed by another session remain pending until their issues reach one of those outcomes.

Identify the first implementation slice: a bounded behavior with a verifiable outcome, small enough for one implementation plan. When a map exists, record its goal and scope in the map's Outcome with planning pending.

Invoke `$handoff` with this next-session focus: use `$code-brain-planning` to plan the first slice, obtain explicit approval, then implement and verify it through that workflow. Supply the source repository path and established base, Code Brain project and map paths, and references to the first slice's scope, supporting ticket notes, and ADRs. Instruct the next session to link the map from the plan's Precedent and the plan from the map's Outcome once the plan exists. Leave later slices for subsequent work.

If the route is already clear during charting, use the same handoff without creating a map; supply the agreed destination and first slice directly.

Report the handoff document's absolute path and end the session. Planning and implementation belong to the new session.

Done when the handoff document exists, its absolute path has been reported, and the map records the next slice when a map exists; or the map explains why the destination was abandoned or superseded.
