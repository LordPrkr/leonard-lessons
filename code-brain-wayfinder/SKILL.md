---
name: code-brain-wayfinder
description: "Chart and resolve an uncertain, multi-session effort through Code Brain decision maps and ticket notes."
disable-model-invocation: true
---

# Code Brain Wayfinder

Use this before `/code-brain-planning` when the destination is clear but the route is not: the work has material decisions that cannot responsibly become one implementation plan yet. It is a decision workflow, not feature delivery.

Each ticket note holds its question, blockers, evidence, and resolution. Use the repository identity and evidence conventions from `/code-brain`.

Read [map and ticket formats](./references/FORMATS.md) before creating or changing a map or ticket.

## Terms

- **Map:** one `wayfinding/<NNN_TOPIC>/map.md` file that names the destination and indexes tickets and resolved decisions.
- **Ticket:** one note under its map's `tickets/` directory; it resolves one decision or directly unblocks one.
- **Frontier:** unresolved tickets whose blockers are resolved.
- **Fog:** in-scope uncertainty that cannot yet be stated as a ticket question.

## 1. Chart the map

1. Read the relevant Code Brain context, ADRs, source evidence, and any existing map and tickets.
2. Establish the destination with the user. It must say what becomes possible when wayfinding ends, not how to build it.
3. Explore breadth-first, separating facts discoverable from source or research from decisions that require the user.
4. Create the numbered map and only the ticket notes whose questions are precise now. Record the remaining in-scope uncertainty as fog and explicit exclusions as out of scope.
5. Link every ticket from the map's Tickets section and record known dependencies in each ticket's Blocked By section.

Done when the destination, initial frontier, known blockers, fog, and out-of-scope boundary are explicit; every ticket is linked from the map; and no feature implementation has started.

## 2. Work one ticket

1. Read the map and ticket notes, then select the named frontier ticket or the first unresolved ticket whose blockers are resolved.
2. Resolve according to type:
   - **Grilling:** ask the user one decision at a time. Do not answer on their behalf.
   - **Research:** use primary sources and record cited findings in the ticket note.
   - **Prototype:** invoke `/tracer-bullet`; link the runnable evidence and its finding.
   - **Task:** perform only the narrow manual work needed to unblock a decision.
3. Record the answer, evidence, and consequences in the ticket note. Add a one-line linked gist to the map's Decisions section.
4. Promote newly precise fog into linked ticket notes. Update dependent tickets and record the reason in the Resolution of any ticket invalidated by the decision.

Done when the selected ticket has a durable resolution, every material claim has evidence, and the map and dependent tickets reflect the newly known route.

## 3. Hand off to planning

When all in-scope tickets are resolved and no material fog remains, create a Code Brain plan through `/code-brain-planning`. Link the map from the plan's Precedent and the plan from the map's Outcome.

If the route is already clear during charting, route directly to `/code-brain-planning`; it creates the implementation plan without a map.

Done when the map either links to its implementation plan or explains why the destination was abandoned or superseded.
