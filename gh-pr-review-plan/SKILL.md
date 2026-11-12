---
name: gh-pr-review-plan
description: "Assess GitHub pull-request feedback with gh. Use when human reviewers request changes, ask implementation questions, or need evidence-backed replies."
---

# GH PR Review Plan

Turn human review feedback on the current branch's PR into a response plan without implementing fixes. Record it in Code Brain's `review/pr-<number>-<short-head-sha>-feedback.md` with `$code-brain-writeback` as you go.

## 1. Pin the PR

Capture the PR's number, URL, base and head SHAs, and merge-base diff with `gh pr view`, asking for the PR when the branch has none.

Done when the pinned target is recorded in the review artifact.

## 2. Collect feedback

Page every review thread, nested comment, review summary, and issue comment through GraphQL until exhausted. Treat human requests for a change, answer, or decision as actionable, and keep author and bot replies as context.

Done when every page is read and each actionable request has its full thread.

## 3. Assess

Inspect the referenced source at the pinned head and classify each request as `valid`, `invalid`, or `needs clarification`, with a one-sentence evidence note.

Done when every request's classification and links are persisted under `Feedback`.

## 4. Plan responses

Merge duplicate requests and write one entry per item in the format below, adding reusable lessons under `Lessons`. Report the artifact path with the plan.

```text
Sources: <comment URLs>
Classification: valid | invalid | needs clarification
Evidence: <source and code evidence>
Smallest change: <files and intended diff, when valid>
Acceptance check: <command or observation, when valid>
Reply: <concise evidence-backed response>
```

Done when every actionable request appears in exactly one entry.
