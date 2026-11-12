---
name: finalize-implementation
description: Finalize verified implementation changes by reviewing delivery readiness, committing conventionally, pushing to GitHub, and creating a labeled pull request with a finished description. Use when work is ready to ship or another workflow needs a commit-and-PR handoff.
---

# Finalize Implementation

When a blocker needs the user, report the failed command, the repair you attempted, and the smallest decision needed.

## 1. Commit

Confirm the work is on a feature branch in its own worktree (invoking `$feature-branch` if not), then commit only the intended changes with `$conventional-commit-message`, hooks enabled and no amending.

**Complete when:** the work is committed and the worktree is clean.

## 2. Rebase and push

Rebase onto the freshly fetched PR base (or default branch), using `$resolving-merge-conflicts` for conflicts and rerunning affected checks. Push with upstream tracking and without force.

**Complete when:** the fetched base is an ancestor of `HEAD`, checks pass, and the remote branch matches `HEAD`.

## 3. Open the pull request

Find or create the branch's PR with a Conventional Commit title scoped to the main package, and write its body with `$spellbinding-sentences` following repository guidance or recent PRs. Apply every label the repository requires.

**Complete when:** exactly one open PR has a finished title, body, and labels, and you have returned its URL with the verification performed.
