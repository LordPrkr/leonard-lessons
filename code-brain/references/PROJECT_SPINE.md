# Project Spine

Use these templates when `/code-brain` initializes a project without `VISION.md`. Do not bulk-create project files. Replace placeholders, omit router links to directories that do not exist, and obtain the user's explicit confirmation before writing `VISION.md`.

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

Read [VISION.md](./VISION.md) before changing strategy. `KANBAN.md` is the authoritative work queue.

## Start here
- [Work board](./KANBAN.md)
- [Plans](./plans/)
- [Domain context](./domain/)
- [Durable notes](./notes/)
- [Resources](./resources/)

## Maintenance
- Keep this file a router, not a backlog.
- Keep task status only in `KANBAN.md`.
- Link only active plans here; remove them when work closes.
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
