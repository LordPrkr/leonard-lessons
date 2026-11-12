---
name: code-brain
description: "Code Brain conventions and project spine. Use when initializing or reconciling Code Brain, configuring a project's issue tracker, or whenever another skill reads or writes its artifacts."
---

# Code Brain

Code Brain is durable project memory at `$CODE_BRAIN_ROOT/<repo>/` (default root `~/Documents/Code Brain`); source repositories stay the evidence and implementation surface. Use Pi's Obsidian tools for vault work.

## Repository identity

Resolve `<repo>` from the target source repository's `origin` basename, falling back to the main worktree's (`git rev-parse --git-common-dir`) origin or top-level basename. Ask for the source path when invoked from the vault or an unrelated repository.

## Project layout

```txt
VISION.md          human-owned purpose, principles, agent authority, non-goals
AGENTS.md          short router to the tracker, active plans, and canonical docs
ISSUE_TRACKER.md   confirmed tracker location and workflow
plans/<NNN_TOPIC>/ plan.md, notes, explanation.md, receipt.md
wayfinding/<NNN_TOPIC>/  decision maps and ticket notes
docs/              canonical Diátaxis docs, routed from docs/README.md
domain/ notes/ resources/ review/ todo/
```

- Create directories lazily, link between artifacts with relative paths, and report the absolute path of every artifact you create.
- Number new folders one past the highest existing prefix, and read legacy `approved: true|false` plan metadata as `approved`|`draft`.
- Task status lives in the configured tracker; Code Brain holds context and links to issues.
- Read relevant `domain/` context and ADRs before planning, use their vocabulary, and surface conflicts with source.
- Name review artifacts `review/pr-<number>-<short-sha>-{feedback,review}.md` or `review/branch-<short-sha>-review.md`, and update them in place on reruns.

## Evidence

Cite each material claim beside it, and for artifacts without inline citations use an `## Evidence` list of `repo: path @ SHA`, `external: URL`, or `code-brain: link` entries with dates. Re-verify repository claims against current source before relying on them.

## Initialize or reconcile

On a bare invocation, audit the spine, router links, active plans, and tracker config, then propose the smallest repair and apply it only after the user confirms. When `VISION.md` is missing, interview the user one question at a time and write the spine from [the templates](./references/PROJECT_SPINE.md) after they confirm it.

## Issue tracker

Read `ISSUE_TRACKER.md` before any tracker operation. When it is missing, incomplete, or the user changes tracker details, inspect representative issues and project groupings in that tracker, show the proposed workflow with cited examples, and save it only after the user confirms.
