---
name: github-pr-description
description: Create or update GitHub pull-request descriptions. Use when the user wants a PR opened, its body written, or its description refreshed from the branch diff.
---

# GitHub PR Description

Apply `/spellbinding-sentences` to the pull-request body.

## 1. Identify the pull request

Use `git` and `gh` to identify the repository, current branch, target branch, and open pull request. Create the pull request if none exists. If GitHub authentication fails, stop and ask the user to authenticate.

**Complete when:** one open pull request and its target branch are known.

## 2. Understand the change

Compare the branch with the pull request's target branch. Read enough changed code and validation evidence to explain the motivation, big-picture mechanisms, reviewer-relevant tradeoffs, and testing. Ask for missing motivation rather than inventing it.

**Complete when:** every substantive section of the pull-request template can be filled from evidence or an explicit `N/A`.

## 3. Fill the template

Use the repository-named template in `references/` when present:

- `frontend-web-monorepo` → `references/frontend-web-monorepo.md`

Otherwise use the repository's configured pull-request template. If neither exists, use `Summary` and `Test plan` sections. Preserve the selected template's heading order exactly, replace every comment and placeholder, and delete only sections the template explicitly marks as optional.

If the user or calling skill supplies an issue URL, place it at the top in the template's issue field or as `**Issue**: <url>`.

**Complete when:** the body contains no unresolved placeholders, describes the change at reviewer level rather than line by line, and includes every known validation result.

## 4. Publish and verify

Update the pull-request body with `gh`, then read it back.

**Complete when:** the open pull request contains the finished body exactly.
