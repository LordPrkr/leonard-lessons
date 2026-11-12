---
name: code-scry
description: "Use when reviewing a GitHub PR, a branch, or committed changes since a commit, tag, or merge-base. Enforces applicable precedent through independent Standards and Spec reviews, proposes diffs, and stages pending inline comments for GitHub PRs through gh."
---

# Code Scry

Review a change on two independent axes, each run in its own subagent so one cannot mask the other: **Standards** (does it follow documented rules and applicable precedent?) and **Spec** (does it implement what was asked?).

**Follow precedent:** existing code and tests with the same responsibility, trust boundary, and lifecycle are enforceable standards, and a departure needs a requirement the pattern cannot meet plus authorization from the task or an approved decision.

## 1. Pin the scope

For a PR, follow [Pin the PR](github-pr-review.md#pin-the-pr). Otherwise diff `git diff <fixed-point>...HEAD` at recorded SHAs, asking for a fixed point when none is given.

**Complete when:** a non-empty diff and commit list are pinned to SHAs.

## 2. Gather sources

Find the spec from the PR description, linked issues, commit references, or a user-supplied path, and ask the user when none exists. Collect documented standards and the closest pre-change implementations and tests; code added by the change cannot be its own precedent.

**Complete when:** the spec (or confirmed absence) and precedent sources with paths and symbols are listed.

## 3. Review in parallel

Launch both subagents at once with the pinned diff, the Follow precedent rule, and the finding format below. Standards gets the precedent sources and also flags Fowler smells as non-blocking judgement calls that yield to precedent; Spec reports missing, wrong, and unrequested behavior, quoting the spec.

**Complete when:** each axis has reported, failed explicitly, or been skipped for lack of a spec.

## 4. Aggregate

Polish each finding with `$spellbinding-sentences` and complete any missing proposed diff, keeping the two axes as separate, unranked reports. Also check the diff for the manual review priorities below, recording each as changed, unchanged, or unverified.

**Complete when:** every actionable finding meets the finding format and every priority category has a status.

## 5. Stage PR comments

For a PR, follow [Stage pending comments](github-pr-review.md#stage-pending-comments); skip this for local reviews.

**Complete when:** every finding is in a verified pending review, linked as already raised, kept in chat, or reported as a delivery failure.

## 6. Respond

Open with what the change accomplishes and how. Then give a manual review guide for each changed priority area with a source link, a short real excerpt, its consequence, and a concrete check. End with the separate Standards and Spec reports, their counts, and the pending review link.

**Complete when:** the user has the overview, manual review guide, both reports, and delivery status.

## Finding format

- Open with a [Conventional Comment](https://conventionalcomments.org/) line, `<label> (blocking|non-blocking): <concrete subject>`, where blocking requires a demonstrated defect, unmet requirement, or precedent breach.
- Explain in plain language what happens, when, why it matters, and what should happen instead, citing the standard, precedent (pre-change path and symbol), or spec line.
- Give the actionable fix as a complete unified diff with `--- a/` and `+++ b/` headers inside `<details><summary>Suggested diff</summary>`.

## Manual review priorities

Order these by how hard the change is to reverse:

- **Backend:** API contracts, database queries, and schema changes.
- **Frontend:** package export contracts and new network requests.
