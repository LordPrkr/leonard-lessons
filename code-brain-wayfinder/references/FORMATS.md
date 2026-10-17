# Map and Ticket Formats

## Map

`wayfinding/<NNN_TOPIC>/map.md` is the low-resolution index. It stores no ticket resolution beyond a one-line linked gist.

```md
# <Destination> Wayfinding

## Destination

<What is clear or possible when this effort is ready for planning.>

## Notes

<Relevant domain context, ADRs, source repositories, and skills.>

## Tickets

- [<ISSUE-ID>: <Ticket title>](<Linear issue URL>)

## Decisions

- [<ISSUE-ID>: <Ticket title>](<Linear issue URL>) — <one-line answer>

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

A ticket is a Linear issue in the configured team and project. Use the following sections in its description; store blockers as Linear issue relations and status through the project's workflow.

```md
# <Ticket title>

## Question

<The precise decision or investigation this ticket resolves.>

## Type

<Grilling | Research | Prototype | Task>

## Resolution

<Write only when resolved. Link to created research or prototype evidence.>

## Consequences

- <New ticket, invalidated ticket, constraint, or `None.`>

## Evidence

- external: <https://example.com> — accessed YYYY-MM-DD
```

A ticket is resolved when its Resolution records an answer or explains why the question was withdrawn, deferred, or superseded. Link reusable findings in Code Brain from the issue and keep enough context in the description to understand the decision without vault access.
