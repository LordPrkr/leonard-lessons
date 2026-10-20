---
name: code-brain
description: "Code Brain conventions and project spine. Use when initializing or reconciling Code Brain, configuring a project's issue tracker, or whenever another skill reads or writes its artifacts."
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
├── ISSUE_TRACKER.md
├── docs/
├── plans/<NNN_TOPIC>/
├── wayfinding/<NNN_TOPIC>/
├── todo/
├── domain/
├── notes/
├── resources/
└── review/
```

Create optional directories and artifacts lazily. Keep each plan and its notes, diagrams, canvases, and receipt in its numbered folder.

Whenever any workflow creates a Code Brain artifact, immediately report its resolved absolute filesystem path to the user. Report every path when one step creates several artifacts. Keep links inside Code Brain portable and relative; absolute paths belong in the user-facing creation report. An artifact-creation step is complete only after every new artifact's absolute path has been reported.

Activity artifacts under `plans/`, `review/`, and `notes/dreams/` preserve provenance. Repo-wide documentation under `docs/` is canonical: update an existing topic document instead of copying the same lesson into another artifact. Create `docs/README.md` with links grouped by reader need when the first canonical document is promoted; link only that landing page from `AGENTS.md` when the router exists.

- `docs/tutorials/` teaches through a guided learning experience.
- `docs/how-to/` gives steps for accomplishing a real task.
- `docs/reference/` describes factual contracts and should mirror the machinery it documents.
- `docs/explanation/` connects concepts, constraints, tradeoffs, and reasons.

Use these as a Diátaxis compass, not a mandatory four-folder scheme: create only the category and topic documents the project needs.

- `VISION.md` is human-owned strategic intent. Read it before durable planning and ask the user before changing it.
- `AGENTS.md` is the short agent-maintained router to canonical memory, active plans, issue-tracker configuration, and project-specific Code Brain rules. It is not a backlog.
- `ISSUE_TRACKER.md` defines this project's issue tracker and the user-confirmed workflow for using it. The configured tracker owns task status; implementation plans use their own frontmatter status for design lifecycle.
- `wayfinding/` holds decision maps and ticket notes for uncertain work; their issues live in the configured tracker.
- `todo/` holds durable context for unplanned work, not one-line task stubs. Simple tasks live in the configured tracker.
- `review/` holds review feedback and evidence-backed lessons. Use `review/pr-<number>-<short-head-sha>-feedback.md` for human feedback assessment, `review/pr-<number>-<short-head-sha>-review.md` for code review, and `review/branch-<short-head-sha>-review.md` for local branch review. Update the same immutable-target artifact across repeated runs of a workflow instead of creating session copies.
- Plans preserve approved design. `receipt.md` links the finalized PR and summarizes review findings and follow-up.

Before a Code-Brain-aware workflow plans or implements, read the relevant `domain/` context and ADRs, use their canonical vocabulary, and surface any conflict with source evidence or the requested direction.

Keep tracked task status in the configured tracker and reference issues from their durable notes. When promoting a todo note, move its useful context into the plan folder, delete the todo note, and update the issue's context link to the plan.

## Issue tracker

Read `ISSUE_TRACKER.md` before using a project's tracker. When the user supplies or changes issue-tracker information, or a workflow needs tracker configuration that is missing or incomplete, follow [issue-tracker setup](./references/ISSUE-TRACKER.md): inspect tracker precedent, confirm the proposed workflow with the user, then persist it. Existing confirmed configuration can be used without repeating setup.

## Plan authoring

When a Code Brain workflow creates or revises an implementation plan, read and apply the [plan authoring contract](./references/PLAN-CONTRACT.md). The calling workflow owns approval, plan status, and receipts.

## Initialization and reconciliation

On bare `$code-brain`, audit the existing project and offer the smallest reconciliation. When `VISION.md` is missing, or the user asks to initialize, audit, repair, or reconcile a project, read [`references/INIT.md`](./references/INIT.md) and follow that branch.

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

Cite source-backed or external claims beside the relevant statement in implementation plans, following the plan authoring contract. For other durable artifacts, use:

```md
## Evidence

- repo: `relative/path.ts` @ `<full SHA>` — inspected YYYY-MM-DD
- external: <https://example.com/spec> — accessed YYYY-MM-DD
- session: `<session id>` — local-only; durable claim summarized above
- code-brain: [source artifact](../relative/path.md) — distilled YYYY-MM-DD
```

Before relying on a material repository claim, verify it against current source. When evidence records a source revision, compare the path at that revision with current `HEAD`. Code Brain artifact links preserve provenance but never replace the underlying repository or external evidence for a material claim. Re-read changed or unavailable evidence. Temporary or absolute machine paths may remain as labeled local leads, but never as the sole evidence for a durable claim. Do not add freshness timers, generated manifests, or automatic rewriting.
