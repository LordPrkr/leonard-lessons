---
name: code-brain-wayfinder
description: "Chart and resolve an uncertain, multi-session effort as decision tickets on the Code Brain Kanban board."
disable-model-invocation: true
---

# Code Brain Wayfinder

Use this before `/code-brain-planning` when the destination is clear but the route is not: the work has material decisions that cannot responsibly become one implementation plan yet. It is a decision workflow, not feature delivery.

`KANBAN.md` is the local issue tracker. A ticket's lane is its only workflow status; its note holds its question, evidence, and resolution. Use the repository identity and evidence conventions from `/code-brain`.

Read [map and ticket formats](./references/FORMATS.md) before creating or changing a map or ticket.

## Terms

- **Map:** one `wayfinding/<NNN_TOPIC>/map.md` file that names the destination and indexes resolved decisions.
- **Ticket:** one note under its map's `tickets/` directory; it resolves one decision or directly unblocks one.
- **Frontier:** unblocked tickets whose cards are in `Ready`.
- **Fog:** in-scope uncertainty that cannot yet be stated as a ticket question.

## 1. Chart the map

1. Read the relevant Code Brain context, ADRs, source evidence, and the existing board.
2. Establish the destination with the user. It must say what becomes possible when wayfinding ends, not how to build it.
3. Explore breadth-first, separating facts discoverable from source or research from decisions that require the user.
4. Create the numbered map and only the ticket notes whose questions are precise now. Record the remaining in-scope uncertainty as fog and explicit exclusions as out of scope.
5. Add one linked card for every ticket to `KANBAN.md`: unblocked tickets to `Ready`; known-blocked tickets to `Blocked`. A card is the ticket claim and status surface.

Done when the destination, initial frontier, known blockers, fog, and out-of-scope boundary are explicit; every ticket has exactly one card; and no feature implementation has started.

## 2. Work one ticket

1. Read the map, then select the named frontier ticket or the first `Ready` ticket. Move its card to `In Progress` before investigating; this claims it.
2. Resolve according to type:
   - **Grilling:** ask the user one decision at a time. Do not answer on their behalf.
   - **Research:** use primary sources and record cited findings in the ticket note.
   - **Prototype:** invoke `/tracer-bullet`; link the runnable evidence and its finding.
   - **Task:** perform only the narrow manual work needed to unblock a decision.
3. Record the answer, evidence, and consequences in the ticket note. Add a one-line linked gist to the map's Decisions section.
4. Close the ticket by moving its card to `Done`. Promote newly precise fog into ticket notes and cards; update or close tickets invalidated by the decision.

Done when the selected ticket has a durable resolution, every material claim has evidence, its card is in `Done`, and the board's frontier reflects the newly known route.

## 3. Hand off to planning

When no frontier tickets or material fog remain, create a Code Brain plan through `/code-brain-planning`. Link the map from the plan's References and the plan from the map's Outcome.

If the route is already clear during charting, do not create a map; route directly to `/pragmatic-plan` or `/code-brain-planning`.

Done when the map either links to its implementation plan or explains why the destination was abandoned or superseded.
