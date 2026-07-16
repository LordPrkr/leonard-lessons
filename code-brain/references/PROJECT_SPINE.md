# Project Spine

Use these templates when `/code-brain` initializes a project without `VISION.md`. See [`EXAMPLE_AGENTS.md`](./EXAMPLE_AGENTS.md) for a filled router. Do not bulk-create project files. Replace placeholders, omit router links to notes that do not exist, and obtain the user's explicit confirmation before writing `VISION.md`.

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

Read [VISION.md](./VISION.md) before changing strategy. `KANBAN.md` is authoritative for durable Code Brain-managed work.

## Start here
- [Vision](./VISION.md)
- [Work board](./KANBAN.md)

## Active plans
- <Relative link to each non-closed plan, or `None.`>

## Canonical memory
- <Relative links to existing context, notes, or resources; omit this section when empty.>

## Maintenance
- Keep this file a router, not a backlog.
- Keep managed task status only in `KANBAN.md`.
- Add plans when work starts; remove them when work closes.
```

## `KANBAN.md`

```md
---
kanban-plugin: board
---

## Inbox

## Ready

## In Progress

## Review

## Blocked

## Done
```
