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
├── plans/       # numbered implementation plans
├── notes/       # scout/context notes
├── canvases/    # current/new behavior sketches
├── diagrams/    # Mermaid diagrams
├── domain/      # glossary, context maps, ADRs
├── resources/   # reusable references, checklists, docs
└── review/      # ingested PR review comments
```

Create folders lazily.

## Numbering

Number plans by scanning `plans/` and incrementing the highest prefix: `001_TOPIC.md`, `002_TOPIC.md`, etc.
