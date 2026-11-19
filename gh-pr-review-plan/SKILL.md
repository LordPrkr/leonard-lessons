---
name: gh-pr-review-plan
description: "Assess GitHub pull-request feedback with gh. Use when human or automated reviewers raise findings, request changes, or ask implementation questions."
---

# GH PR Review Plan

Turn review feedback on the current branch's PR into a response plan without implementing fixes. Use `$code-brain` for the `review/pr-<number>-<short-head-sha>-feedback.md` artifact and `$code-brain-writeback` for evidence and revisions. For this workflow, write once after collection, once after assessing each group, and once for the finished plan.

## 1. Pin the PR

Run `gh pr view --json number,url,baseRefOid,headRefOid,author`. Ask for the PR if the branch has none. Fetch missing commits, then run `git merge-base <base-sha> <head-sha>` and use `git diff <merge-base> <head-sha>` for the pinned diff.

Done when the PR number, URL, base, head, and merge base are known.

## 2. Collect feedback

Use one `gh api graphql` request for the first pages of `reviewThreads` (including each thread's first `comments` page), `reviews`, and PR `comments`. Request `pageInfo { hasNextPage endCursor }` on every connection and follow cursors only where `hasNextPage` is true.

Evaluate every comment and review summary for findings or requests for a change, answer, or decision, regardless of who posted it. Carry those items forward as actionable; keep routine status updates and purely informational replies as context. Group items that share a claim or requested outcome and can be decided using the same evidence. Keep every source URL and its context in the group. Follow [Reuse prior assessments](reuse-assessments.md) to record each group's fingerprint and check any existing assessments for this PR head.

Done when all connections are exhausted, every comment and review summary has been screened, every actionable item belongs to a group with its full context, and the target and grouped inventory are saved.

## 3. Assess

For each group without a reusable assessment, inspect the referenced source at the pinned head and classify the group as `valid`, `invalid`, or `needs clarification`, with a one-sentence evidence note.

Done when every group's classification, evidence, and source links are persisted under `Feedback`.

## 4. Plan responses

Write one entry per group in the format below, adding reusable lessons under `Lessons`. Report the artifact path with the plan.

```text
Sources: <comment URLs>
Classification: valid | invalid | needs clarification
Evidence: <source and code evidence>
Smallest change: <files and intended diff, when valid>
Acceptance check: <command or observation, when valid>
Reply: <concise evidence-backed response>
```

Done when every actionable item appears in exactly one entry.
