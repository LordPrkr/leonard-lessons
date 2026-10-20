# Map and Ticket Formats

## Map

`wayfinding/<NNN_TOPIC>/map.md` is the low-resolution index. It stores no ticket resolution beyond a one-line linked gist.

```md
# <Destination> Wayfinding

## Destination

<What is clear or possible when this effort is ready for planning.>

## Notes

<Relevant domain context, ADRs, source repositories, and skills.>

## Decisions

- [<Ticket title>](./tickets/001-example.md) — <one-line answer>

## Fog

- <In-scope uncertainty that is not yet a precise question.>

## Out of Scope

- <Consciously excluded work and why.>

## Outcome

- <Link to the implementation plan, or why this effort ended.>

## Evidence

- repo: `<path>` @ `<full SHA>` — inspected YYYY-MM-DD
```

## Ticket

`wayfinding/<NNN_TOPIC>/tickets/<NNN_SLUG>.md` is the detailed, durable record for one decision.

```md
# <Ticket title>

## Issue

<URL or stable ID of the issue in the project's configured tracker.>

## Question

<The precise decision or investigation this ticket resolves.>

## Type

<Grilling | Research | Prototype | Task>

## Blocked By

- <Relative link to each blocking ticket, or `None.`>

## Resolution

<Write only when resolved. Link to created research or prototype evidence.>

## Consequences

- <New ticket, invalidated ticket, constraint, or `None.`>

## Evidence

- external: <https://example.com> — accessed YYYY-MM-DD
```

The linked issue owns workflow status under the project's `ISSUE_TRACKER.md`. Keep the note's Blocked By links aligned with tracker dependencies; record workflow status only in the tracker.
