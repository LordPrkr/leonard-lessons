---
name: code-brain
description: "Canonical Code Brain contract for durable project memory, project bootstrap, evidence, repository identity, and Obsidian Kanban ownership. Use whenever another skill reads or writes Code Brain artifacts."
---

# Code Brain

Code Brain is durable project memory; source repositories remain the evidence and implementation surface. Use Pi's Obsidian tools directly for vault work.

Resolve the vault root from non-empty `CODE_BRAIN_ROOT`, otherwise use `~/Documents/Code Brain`. The project folder is `$CODE_BRAIN_ROOT/<repo>/`.

## Repository identity

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
- `KANBAN.md` is the authoritative local workflow state. Its lanes are Inbox, Ready, In Progress, Review, Blocked, and Done.
- `todo/` holds unplanned context. Cards link to todo notes; promotion to a numbered plan replaces the card target with that plan.
- Plans preserve approved design. Appendable `receipt.md` files preserve execution truth.

Cards are plain Markdown wikilinks:

```md
- [ ] [[todo/Migrate to oxlint]]
- [ ] [[plans/020_AUTH_REFACTOR/plan|Implement auth refactor]]
```

The card lane is the only task-status source. Task notes do not copy lane state into frontmatter; plan status describes design lifecycle, not board lane. Direct block links are exceptional.

## Project bootstrap

Ordinary reads may use legacy projects. When initializing durable planning for a project without `VISION.md`:

1. Read existing Code Brain artifacts and the source repository's README, AGENTS files, and relevant docs.
2. Interview the user one question at a time until Purpose, Agent authority, and Non-goals are explicit.
3. Obtain explicit confirmation of `VISION.md`.
4. Read [`references/PROJECT_SPINE.md`](references/PROJECT_SPINE.md), then write all three project files from its templates, omitting links to directories that do not exist.
5. Resume the calling workflow.

Do not invent strategic intent or bulk-bootstrap legacy projects.

Done when all three project files exist, the user confirmed `VISION.md`, every `AGENTS.md` router link resolves, and `KANBAN.md` contains all six initialized lanes.

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
