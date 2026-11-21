# GitHub PR review

Use the PR's base repository for every `gh` call, qualifying `--repo <host>/<owner/repo>` and `gh api --hostname` on non-default hosts.

## Pin the PR

Capture metadata with `gh pr view --json url,number,title,body,author,baseRefOid,headRefOid,commits,closingIssuesReferences` and save `gh pr diff --color never`, recapturing if either SHA moves. Read supporting source at the pinned head through `gh api` or an isolated checkout.

**Complete when:** a non-empty saved diff matches the recorded SHAs.

## Deliver PR comments

1. Page `pulls/<n>/comments`, `pulls/<n>/reviews`, and `issues/<n>/comments`, and drop findings whose concern any reviewer already raised, keeping its link for chat.
2. Anchor each remaining finding to its smallest diff range (`RIGHT` for new lines, `LEFT` for removed, or a file-level thread), adding a GitHub `suggestion` block for self-contained replacements. Findings about files outside the PR stay in chat.
3. Compare the PR's `author.login` with the authenticated login from `gh api --hostname <host> user --jq .login`. Auto-submit only when both logins are known and match. For this path, reuse a same-head draft only if its body and threads are all from code-scry. If an unrelated draft prevents staging a separate review, leave it intact and report the findings in chat with the blocker.
4. Reuse the authenticated account's eligible `PENDING` review at the same head, or create one with `gh api --method POST repos/<o>/<r>/pulls/<n>/reviews --input payload.json`, setting `commit_id` to the pinned head and omitting `event`. Add threads with the GraphQL `addPullRequestReviewThread` mutation using JSON input files, then read the review and its comments back to verify every thread.
5. When the logins match and the PR still points to the pinned head, submit the verified review immediately with `gh api --method POST repos/<o>/<r>/pulls/<n>/reviews/<review-id>/events -f event=COMMENT`. Verify the review state is `COMMENTED`. When authorship differs or is unknown, leave the review `PENDING` for the user. Report the review URL, state, and verified comment count, or the failure that prevented delivery.

Set the root body to one short sentence per axis, replacing any earlier agent summary:

```markdown
## Standards

1 blocking finding.

## Spec

No findings.
```

Each comment body is the finding (opening line, discussion, collapsed diff) followed by: *This feedback was provided by an agent; please confirm the reasoning and suggested change.*

**Complete when:** every finding is accounted for in verified review content, linked existing feedback, chat, or an explicit failure.
