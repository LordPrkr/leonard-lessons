# Project Spine

Use these templates when `$code-brain` initializes a project without `VISION.md`. See [`EXAMPLE_AGENTS.md`](./EXAMPLE_AGENTS.md) for a filled router. Do not bulk-create project files. Replace placeholders, omit router links to notes that do not exist, obtain the user's explicit confirmation before writing `VISION.md`, and follow [issue-tracker setup](./ISSUE-TRACKER.md) before writing tracker configuration.

## `VISION.md`

```md
# <Project> Vision

## Purpose
<Why the project exists and who it serves.>

## Principles
- <Durable product or architectural principle.>

## Agent authority
### May do
- <Autonomous action.>

### Ask first
- <Human-owned or risky decision.>

## Non-goals
- <Explicit boundary.>
```

## `AGENTS.md`

```md
# <Project> Code Brain

Read [VISION.md](./VISION.md) before changing strategy. [ISSUE_TRACKER.md](./ISSUE_TRACKER.md) defines where work is tracked and how to use that tracker.

## Start here
- [Vision](./VISION.md)
- [Issue tracker](./ISSUE_TRACKER.md)

## Active plans
- <Relative link to each non-closed plan, or `None.`>

## Canonical memory
- <Relative links to existing context, notes, or resources; omit this section when empty.>

## Maintenance
- Keep this file a router, not a backlog.
- Keep tracked task status in the configured issue tracker.
- Add plans when work starts; remove them when work closes.
```

## `ISSUE_TRACKER.md`

```md
# <Project> Issue Tracker

## Location and access
<Tracker, exact repository/project/team URL or identifier, and available tools or commands.>

## Workflow
<Confirmed conventions for finding and creating issues, issue structure, ownership, ordering, status transitions, dependencies, and resolution or cancellation.>

## Code Brain context
<How issues reference durable context and how notes record issue URLs or stable IDs.>

## Evidence
- <Representative issue or workflow-guidance link, observed convention, and inspection date.>
- <User-confirmed choice or explicit evidence gap, when applicable.>
```
