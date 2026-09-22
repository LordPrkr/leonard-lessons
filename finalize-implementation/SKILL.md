---
name: finalize-implementation
description: Finalize verified implementation changes by reviewing delivery readiness, committing conventionally, pushing to GitHub, and creating a labeled pull request with a finished description. Use when work is ready to ship or another workflow needs a commit-and-PR handoff.
---

# Finalize Implementation

When a delivery blocker requires a user decision, report the exact failed command, attempted repair, and smallest decision needed. Create a draft pull request only when the user requests visibility before that blocker is resolved.

## 1. Confirm the delivery workspace

Confirm the intended work is on the current feature branch in an independently provisioned worktree. Invoke `/feature-branch` only when that branch or workspace has not already been established.

**Complete when:** the intended work is assigned to the current feature branch in its provisioned worktree.

## 2. Review the net diff

Review the complete branch diff against the request, repository standards, correctness, and simplicity. Resolve actionable findings and rerun affected checks.

**Complete when:** every retained diff hunk is justified and required checks still pass.

## 3. Refresh the base branch

Determine whether the feature branch needs to refresh or rebase onto its base branch under repository practice. When it does, refresh it, resolve any conflicts, and rerun affected checks before delivery.

**Complete when:** the branch is current enough for repository delivery practice and any refresh has passing affected checks.

## 4. Commit and push

Invoke `/conventional-commit-message`, stage only the intended changes, and create one coherent commit with repository hooks enabled, without amending any existing commit. If the work is already committed, do not create an empty commit. Push the branch to `origin` and set its upstream without force-pushing.

**Complete when:** the intended commit exists on the tracked GitHub branch.

## 5. Ensure the pull request exists

Use `gh` to find an open pull request for the current branch. If none exists, create one against the default branch and retain its URL. Give the new pull request a Conventional Commit title based on the complete branch diff. When one package is the main target, use its package name as the scope; otherwise omit the scope unless repository precedent supplies one. If an existing pull request title is not Conventional Commit style, update it before continuing.

**Complete when:** exactly one open pull request targets the default branch, and its title uses Conventional Commit style with the main package as its scope when applicable.

## 6. Describe and label the pull request

Invoke `/spellbinding-sentences` before drafting. Infer the body structure from the repository's pull-request guidance; when that guidance does not prescribe one, use recent comparable pull requests as precedent. If neither source supplies a structure, ask the user which body structure to use before drafting. Write from the complete branch diff and update it with `gh`; when the pull request already existed, cover every substantive newly committed behavior. Mechanical changes with no reviewer impact need not be called out. Apply every label required by repository guidance.

**Complete when:** the pull-request title uses Conventional Commit style, the description matches the branch and selected repository or user-provided structure, neither contains unresolved placeholders, and every required label is applied.

## 7. Return the pull request

Read the published pull request back with `gh` and return its URL and verification performed.

**Complete when:** the user has a working pull-request link and its delivery verification.
