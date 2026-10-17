---
name: code-brain-wayfinder
description: "Chart and resolve an uncertain, multi-session effort through Code Brain decision maps and Linear issues."
disable-model-invocation: true
---

# Code Brain Wayfinder

Use this before `/code-brain-planning` when the destination is clear but the route is not: the work has material decisions that cannot responsibly become one implementation plan yet. It is a decision workflow, not feature delivery.

Use `/code-brain` for repository identity, evidence, and the configured Linear workflow. Each decision ticket is a Linear issue holding its question, blockers, evidence, and resolution.

Read [map and ticket formats](./references/FORMATS.md) before creating or changing a map or ticket.

## Terms

- **Map:** one `wayfinding/<NNN_TOPIC>/map.md` file that names the destination and indexes tickets and resolved decisions.
- **Ticket:** one Linear issue that resolves one decision or directly unblocks one.
- **Frontier:** unresolved tickets whose blockers are resolved, using the configured Linear workflow.
- **Fog:** in-scope uncertainty that cannot yet be stated as a ticket question.

## 1. Chart the map

1. Read the relevant Code Brain context, ADRs, source evidence, and any existing map and linked Linear issues.
2. Establish the destination with the user. It must say what becomes possible when wayfinding ends, not how to build it.
3. Explore breadth-first, separating facts discoverable from source or research from decisions that require the user.
4. Create the numbered map and create or reuse Linear issues only for questions that are precise now. Record the remaining in-scope uncertainty as fog and explicit exclusions as out of scope.
5. Link every issue from the map's Tickets section and record known dependencies with Linear issue relations.

Done when the destination, initial frontier, known blockers, fog, and out-of-scope boundary are explicit; every ticket is linked from the map; and no feature implementation has started.

## 2. Work one ticket

1. Read the map and linked Linear issues, select the named frontier ticket or the first unresolved ticket whose blockers are resolved, and start it according to the project's workflow.
2. Resolve according to type:
   - **Grilling:** ask the user one decision at a time. Do not answer on their behalf.
   - **Research:** use primary sources and record cited findings in the issue.
   - **Prototype:** invoke `/tracer-bullet`; link the runnable evidence and its finding.
   - **Task:** perform only the narrow manual work needed to unblock a decision.
3. Record the answer, evidence, and consequences in the issue and close it according to the configured workflow. Add a one-line linked gist to the map's Decisions section.
4. Promote newly precise fog into linked Linear issues. Update dependent issues and explain why any ticket is withdrawn, deferred, or superseded before applying the appropriate workflow state.

Done when the selected issue has a durable resolution and the appropriate Linear status, every material claim has evidence, and the map and dependent issues reflect the newly known route.

## 3. Hand off to planning

When all in-scope tickets are resolved and no material fog remains, create a Code Brain plan through `/code-brain-planning`. Link the map from the plan's Precedent and the plan from the map's Outcome.

If the route is already clear during charting, route directly to `/code-brain-planning`; it creates the implementation plan without a map.

Done when the map either links to its implementation plan or explains why the destination was abandoned or superseded.
