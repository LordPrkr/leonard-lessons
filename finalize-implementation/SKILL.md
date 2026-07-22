---
name: finalize-implementation
description: Finalize verified implementation changes by choosing a feature branch, committing conventionally, pushing to GitHub, preparing the pull request, and optionally linking Jira. Use when work is ready to ship or another workflow needs a commit-and-PR handoff.
---

# Finalize Implementation

## 1. Choose the branch

Inspect the intended diff, current and default branches, open pull request, and recent local, remote, and merged-PR branch names. Do not include unrelated changes.

If the current branch is the default branch, create a feature branch whose shape follows repository precedent. If the current branch is already a feature branch and the changes clearly belong to its existing commits or pull request, keep it. If ownership is unclear, ask whether to use the current branch or create a new one before changing branches. Ask for a branch name only when repository precedent is insufficient.

**Complete when:** every intended change and no unrelated change is assigned to one current feature branch.

## 2. Commit and push

Invoke `/conventional-commit-message`, stage only the intended changes, and create one coherent commit. If the work is already committed, do not create an empty commit. Push the branch to `origin` and set its upstream without force-pushing. Stop with the authentication or remote error if the push fails.

**Complete when:** the intended commit exists on the tracked GitHub branch.

## 3. Ensure the pull request exists

Use `gh` to find an open pull request for the current branch. If none exists, create one against the default branch and retain its URL. Stop and ask the user to authenticate if `gh` cannot access GitHub.

**Complete when:** exactly one open pull request targets the default branch.

## 4. Resolve Jira and describe the pull request

Ask the user for one of: an existing Jira key or URL, permission to create a Jira ticket, or `none`.

- For `none`, invoke `/gh-pr-description`.
- To create a ticket, invoke `/work-documentation-generator`.
- For an existing ticket, resolve its URL and invoke `/gh-pr-description` with that URL.

When the pull request already existed, require its updated description to cover every substantive newly committed behavior. Mechanical changes with no reviewer impact need not be called out.

**Complete when:** the pull-request description matches the branch, links the selected Jira ticket when one exists, and contains no unresolved placeholders.

## 5. Return the artifacts

Read the published pull request back with `gh`. Return the pull-request URL and the Jira URL, or state `Jira: none` when the user declined one.

**Complete when:** the user has working links to every created or updated artifact.
