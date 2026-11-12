# GitHub PR review

Use the PR's base repository for every `gh` call, qualifying `--repo <host>/<owner/repo>` and `gh api --hostname` on non-default hosts.

## Pin the PR

Capture metadata with `gh pr view --json url,number,title,body,baseRefOid,headRefOid,commits,closingIssuesReferences` and save `gh pr diff --color never`, recapturing if either SHA moves. Read supporting source at the pinned head through `gh api` or an isolated checkout.

**Complete when:** a non-empty saved diff matches the recorded SHAs.

## Stage pending comments

1. Page `pulls/<n>/comments`, `pulls/<n>/reviews`, and `issues/<n>/comments`, and drop findings whose concern any reviewer already raised, keeping its link for chat.
2. Anchor each remaining finding to its smallest diff range (`RIGHT` for new lines, `LEFT` for removed, or a file-level thread), adding a GitHub `suggestion` block for self-contained replacements. Findings about files outside the PR stay in chat.
3. Reuse your existing `PENDING` review at the same head, or create one with `gh api --method POST repos/<o>/<r>/pulls/<n>/reviews --input payload.json` (no `event`), then add threads with the GraphQL `addPullRequestReviewThread` mutation using JSON input files. Leave the review pending for the user to submit.
4. Read the review and its comments back to verify every thread, and report the review URL and saved count.

Set the root body to one short sentence per axis, replacing any earlier agent summary:

```markdown
## Standards

1 blocking finding.

## Spec

No findings.
```

Each comment body is the finding (opening line, discussion, collapsed diff) followed by: *This feedback was provided by an agent; please confirm the reasoning and suggested change.*

**Complete when:** every finding is accounted for in verified review content, linked existing feedback, chat, or an explicit failure.
