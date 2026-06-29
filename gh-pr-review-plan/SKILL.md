---
name: gh-pr-review-plan
description: "GitHub PR review planning with gh: pull human reviewer comments from the current branch's associated pull request, assess each comment's validity, plan valid fixes, and draft concise pushback for invalid comments."
---

# GH PR Review Plan

Use `gh` to turn human reviewer comments on the current branch's associated
pull request into a response plan. Do not implement fixes in this skill.

## Steps

### 1. Locate the PR

Run:

```bash
gh pr view --json number,url,headRefName,baseRefName,title,author
```

If no PR is associated with the current branch, ask for the PR URL or number.

Done when the PR number and URL are known.

### 2. Pull human review comments

Get review threads, review summaries, and issue comments. Prefer this GraphQL
query because it preserves resolved state and inline locations:

```bash
OWNER=$(gh repo view --json owner --jq .owner.login)
REPO=$(gh repo view --json name --jq .name)
PR=$(gh pr view --json number --jq .number)

gh api graphql -f owner="$OWNER" -f repo="$REPO" -F number="$PR" -f query='
query($owner: String!, $repo: String!, $number: Int!) {
  repository(owner: $owner, name: $repo) {
    pullRequest(number: $number) {
      url
      reviewThreads(first: 100) {
        pageInfo { hasNextPage endCursor }
        nodes {
          isResolved
          path
          line
          originalLine
          comments(first: 50) {
            pageInfo { hasNextPage endCursor }
            nodes {
              author { login }
              body
              createdAt
              url
            }
          }
        }
      }
      reviews(first: 100) {
        pageInfo { hasNextPage endCursor }
        nodes {
          author { login }
          state
          body
          submittedAt
          url
        }
      }
      comments(first: 100) {
        pageInfo { hasNextPage endCursor }
        nodes {
          author { login }
          body
          createdAt
          url
        }
      }
    }
  }
}'
```

If any `pageInfo.hasNextPage` is true, rerun with cursors before judging.
Ignore comments from bots and the PR author unless the user asks otherwise.
Keep resolved threads only when they contain unresolved follow-up or explain
reviewer intent.

Done when every page is exhausted and every human reviewer comment is listed
once with author, URL, file/line when present, and resolved/unresolved state.

### 3. Assess validity

For each comment, inspect the referenced code before judging. Classify it:

- `valid` — the reviewer found a real bug, risk, requirement miss,
  maintainability issue, or clearer fit with existing patterns.
- `invalid` — the suggestion is factually wrong, already handled, conflicts
  with requirements, or costs more complexity than it saves.
- `needs clarification` — the comment cannot be fairly judged from repo evidence.

Done when every comment has a classification and a one-sentence evidence note.

### 4. Make the response plan

For each comment:

- If `valid`, write the smallest plan to address it: files to change,
  intended diff, and the smallest verification command.
- If `invalid`, draft a concise GitHub reply explaining why not to address it,
  with evidence.
- If `needs clarification`, draft the exact question to ask.

Group duplicate comments under one plan item.

Done when the final plan covers every human reviewer comment exactly once and
contains no implementation changes.
