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

Invoke `/conventional-commit-message`, stage only the intended changes, and create one coherent commit without amending any existing commit. If the work is already committed, do not create an empty commit. Push the branch to `origin` and set its upstream without force-pushing. Stop with the authentication or remote error if the push fails.

**Complete when:** the intended commit exists on the tracked GitHub branch.

## 3. Ensure the pull request exists

Use `gh` to find an open pull request for the current branch. If none exists, create one against the default branch and retain its URL. Give the new pull request a Conventional Commit title based on the complete branch diff. When one package is the main target, use its package name as the scope; otherwise omit the scope unless repository precedent supplies one. Stop and ask the user to authenticate if `gh` cannot access GitHub.

**Complete when:** exactly one open pull request targets the default branch, and any newly created pull request has a Conventional Commit title with the main package as its scope when applicable.

## 4. Resolve Jira and describe the pull request

Assume `Jira: none` without prompting unless the user has already mentioned a Jira ticket or asked to create one.

- For no Jira ticket, invoke `/gh-pr-description`.
- To create a ticket, invoke `/work-documentation-generator`.
- For an existing ticket, resolve its URL and invoke `/gh-pr-description` with that URL.

When the pull request already existed, require its updated description to cover every substantive newly committed behavior. Mechanical changes with no reviewer impact need not be called out.

**Complete when:** the pull-request description matches the branch, links the user-mentioned Jira ticket when one exists, and contains no unresolved placeholders.

## 5. Return the artifacts

Read the published pull request back with `gh`. Return the pull-request URL and the Jira URL, or state `Jira: none` when there is no ticket.

**Complete when:** the user has working links to every created or updated artifact.
