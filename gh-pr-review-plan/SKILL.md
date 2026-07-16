---
name: gh-pr-review-plan
description: "GitHub PR review planning with gh: collect complete review context, assess human comments, plan valid fixes, and draft concise evidence-backed replies."
---

# GH PR Review Plan

Use `gh` to turn human reviewer feedback on the current branch's pull request into a response plan. Do not implement fixes in this skill.

## Steps

### 1. Pin the PR

Run:

```bash
gh pr view --json number,url,headRefName,baseRefName,headRefOid,baseRefOid,title,author
```

Resolve and record the PR head SHA, base SHA, merge base, `git diff <merge-base>...<head-sha>`, and commit list. If no PR is associated with the current branch, ask for its URL or number.

Done when the PR number, URL, and immutable base/head review target are known.

### 2. Collect complete review context

Collect review threads, every nested thread comment, review summaries, and issue comments. Use GraphQL cursor loops: page `reviewThreads`, `reviews`, and issue `comments` until each `hasNextPage` is false; then page every thread's `comments` independently until exhausted. Include each comment's author, body, URL, timestamp, commit OID, path, line, original line, outdated state, and thread resolved state.

Preserve PR-author and bot replies as context. Select only eligible human reviewer requests as actionable items unless the user asks otherwise. Keep resolved threads when their context affects an actionable request or explains reviewer intent.

Done when every connection and nested thread-comment page is exhausted and every actionable request retains its complete conversational context.

### 3. Assess validity

For each actionable request, inspect the referenced source at the pinned head before judging. Classify it:

- `valid` — the reviewer found a real bug, risk, requirement miss, maintainability issue, or clearer fit with existing patterns.
- `invalid` — the suggestion is factually wrong, already handled, conflicts with requirements, or costs more complexity than it saves.
- `needs clarification` — repository evidence cannot fairly decide the request.

Done when every actionable request has a classification, one-sentence evidence note, and links to its source comment and relevant code.

### 4. Make the response plan

Group duplicate requests under one canonical item while retaining every source URL. For each item include:

```text
Sources: <comment URLs>
Classification: valid | invalid | needs clarification
Evidence: <source and code evidence>
Current → desired behavior: <only when valid>
Smallest change: <files and intended diff, only when valid>
Acceptance check: <independently verifiable command or observation, only when valid>
Reply: <concise evidence-backed GitHub response>
Question: <exact question, only when clarification is needed>
```

Done when the final plan covers every actionable human request exactly once, preserves contextual replies, and contains no implementation changes.
