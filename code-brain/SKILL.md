---
name: code-brain
description: "Code Brain conventions for storing durable project docs. Use when another skill writes Code Brain artifacts, or when the user asks where plans, domain notes, ADRs, resources, or review notes belong."
---

# Code Brain

Use `~/Documents/Code Brain/<repo>/` as the project folder. Code Brain stores durable memory; source repos stay evidence and implementation.

Use Obsidian tools directly for Code Brain work: `obsidian_read`, `obsidian_write`, `obsidian_list_notes`, `obsidian_search`, `obsidian_create_mermaid`, and `obsidian_create_canvas`.

## Repo Resolution

Resolve `<repo>` by canonical repository name, not worktree directory name:

1. Use the git remote basename: `git remote get-url origin`, stripping `.git`.
   - `https://github.com/org/front-end-web-monorepo.git` → `front-end-web-monorepo`
2. If no remote exists and the path looks like `~/code/<repo>/<worktree>`, use `<repo>`.
3. Otherwise use the git top-level directory basename.

Never use generic worktree folder names like `main`, `develop`, `review`, or `test` when a remote or parent repo name is available.

## Structure

```txt
~/Documents/Code Brain/<repo>/
├── plans/
│   └── 001_TOPIC/
│       ├── plan.md
│       ├── notes.md
│       ├── call-stack.diagram.md
│       ├── current.canvas
│       └── proposed.canvas
├── notes/       # durable notes unrelated to a specific plan
├── domain/      # glossary, context maps, ADRs
├── resources/   # reusable references, checklists, docs
└── review/      # ingested PR review comments
```

Keep each plan and its notes, diagrams, and canvases together in its named folder. Use descriptive kebab-case names for optional `.diagram.md` and `.canvas` files. Create folders and optional artifacts lazily.

## Numbering

Number plan folders by scanning `plans/` and incrementing the highest prefix across both folders and legacy plan files: `001_TOPIC/`, `002_TOPIC/`, etc. Do not migrate legacy plans unless asked.
