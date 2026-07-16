---
name: code-brain
description: "Code Brain conventions and project spine. Use when initializing or reconciling Code Brain, or whenever another skill reads or writes its artifacts."
---

# Code Brain

Code Brain is durable project memory; source repositories remain the evidence and implementation surface. Use Pi's Obsidian tools directly for vault work.

Resolve the vault root from non-empty `CODE_BRAIN_ROOT`, otherwise use `~/Documents/Code Brain`. The project folder is `$CODE_BRAIN_ROOT/<repo>/`.

## Repository identity

Invoke Code Brain from the target source repository or one of its worktrees. If the current directory is the vault or an unrelated repository, require the target source path before continuing; never use the vault repository itself as `<repo>`.

Resolve `<repo>` with Git, not worktree directory heuristics:

1. Read `origin` from the current worktree. For HTTPS and SCP-style SSH URLs, use the remote repository basename without `.git`.
2. Without a usable origin, run `git rev-parse --path-format=absolute --git-common-dir`. Follow the common directory to the main repository and use its `origin` when available, otherwise its top-level basename.
3. Only then use the current Git top-level basename.

Never infer identity from home-directory layout or generic worktree names.

## Project contract

```txt
$CODE_BRAIN_ROOT/<repo>/
├── VISION.md
├── AGENTS.md
├── KANBAN.md
├── plans/<NNN_TOPIC>/
├── todo/
├── domain/
├── notes/
├── resources/
└── review/
```

Create optional directories and artifacts lazily. Keep each plan and its notes, diagrams, canvases, and receipt in its numbered folder.

- `VISION.md` is human-owned strategic intent. Read it before durable planning and ask the user before changing it.
- `AGENTS.md` is the short agent-maintained router to canonical memory, active plans, the board, and project-specific Code Brain rules. It is not a backlog.
- `KANBAN.md` is the authoritative workflow state for durable Code Brain-managed work. Ordinary work that needs no durable artifact may remain outside it. Its lanes are Inbox, Ready, In Progress, Review, Blocked, and Done.
- `todo/` holds durable context for unplanned work, not one-line task stubs. Simple tasks stay inline on the board.
- Plans preserve approved design. Appendable `receipt.md` files preserve execution truth.

Before a Code-Brain-aware workflow plans or implements, read the relevant `domain/` context and ADRs, use their canonical vocabulary, and surface any conflict with source evidence or the requested direction.

Cards are plain Markdown tasks with an optional wikilink:

```md
- [ ] Migrate both repositories to oxlint
- [ ] [[todo/OAuth provider research]]
- [ ] [[plans/020_AUTH_REFACTOR/plan|Implement auth refactor]]
```

Each managed task appears in exactly one lane. The card lane is its only task-status source; task notes do not copy lane state into frontmatter, and plan status describes design lifecycle rather than board lane. When promoting a todo note, move its useful context into the plan folder, delete the todo note, and replace the card target with the plan. Direct block links are exceptional.

## Initialization and reconciliation

On bare `/code-brain`, audit the existing project and offer the smallest reconciliation. When `VISION.md` is missing, or the user asks to initialize, audit, repair, or reconcile a project, read [`references/INIT.md`](./references/INIT.md) and follow that branch.

## Numbering and compatibility

Number plan folders by scanning `plans/` and incrementing the highest prefix across folders and legacy plan files: `001_TOPIC/`, `002_TOPIC/`, and so on. Do not renumber or migrate historical plans unless asked.

Read legacy metadata without rewriting it:

```text
approved: true  → approved
approved: false → draft
missing         → unknown
```

Never infer implementation from plan age or approval.

## Evidence

When a durable artifact makes a source-backed or external claim, use:

```md
## Evidence

- repo: `relative/path.ts` @ `<full SHA>` — inspected YYYY-MM-DD
- external: <https://example.com/spec> — accessed YYYY-MM-DD
- session: `<session id>` — local-only; durable claim summarized above
```

Before relying on a material repository claim, compare the recorded path at its source revision with current `HEAD`. Re-read changed or unavailable evidence. Temporary or absolute machine paths may remain as labeled local leads, but never as the sole evidence for a durable claim. Do not add freshness timers, generated manifests, or automatic rewriting.
