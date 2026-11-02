# GitHub PR review

Use `gh pr view`, `gh pr diff`, and `gh api` for GitHub review work. Resolve the PR URL or number to an explicit host, base repository, and PR number; use the base repository for PR metadata, diffs, and review writes, including fork PRs. For a non-default GitHub host, qualify `--repo` as `<host>/<owner/repo>` and pass `--hostname` to `gh api`.

## Pin the PR

1. Capture PR metadata with `gh pr view <number> --repo <owner/repo> --json url,number,title,body,baseRefOid,headRefOid,headRepository,headRepositoryOwner,commits,closingIssuesReferences`. Fetch linked GitHub issues with `gh issue view` in their owning repositories.

   **Complete when:** the PR identity, base and head SHAs, commit list, description, and linked issue contents are recorded, or a fetch failure is reported.

2. Save `gh pr diff <number> --repo <owner/repo> --color never` as the review diff. Re-read the base and head SHAs after capture; if either changed, recapture metadata and diff. Read supporting source at the pinned revision through `gh api` or an isolated checkout of the PR head. Local `HEAD` is only usable when it matches that revision.

   **Complete when:** the saved diff corresponds to unchanged captured SHAs and is non-empty, or the empty diff or capture failure is reported.

## Stage pending comments

If there are no actionable findings, skip new threads. Refresh an existing agent-authored pending summary when its outcome has changed or it does not match the summary format; otherwise skip posting.

1. Follow [Check existing feedback](#check-existing-feedback) and exclude findings already raised by any reviewer. Map each remaining finding to the reviewed PR. Compose bodies using [Comment body](#comment-body); keep axis labels in the review summary. Use the repository-relative `path`, file `line`, and diff `side`: `RIGHT` for added/current lines and `LEFT` for removed lines. For ranges, supply the first line and side as well as the final line and side. Anchor to the smallest relevant range in the saved diff. For a changed file without a suitable line anchor, use a file-level thread; findings about files outside the PR belong in the final chat response with their file names and proposed diffs.

   For a self-contained replacement of an anchored `RIGHT` range, also include a GitHub `suggestion` fenced block inside the same collapsed block, containing exactly the replacement for that entire range. Broader changes retain their proposed unified diffs.

   **Complete when:** each finding is either excluded with a link to existing feedback, has a valid line or file anchor, or is retained for chat because its file is outside the PR; every retained body meets the comment format and every suggestion matches its anchored range. If all findings are duplicates, skip new threads and report their links in chat.

2. Re-read the PR base and head SHAs before writing. If either moved, refresh the review and revalidate findings and anchors. Refresh the existing-feedback check immediately before writing, excluding any newly raised duplicates. If the check is incomplete or fails, report the delivery failure and keep findings local until duplicate coverage can be verified. Use `gh api user` and paginated `gh api repos/<owner>/<repo>/pulls/<number>/reviews` to check for the authenticated user's existing `PENDING` review. Read its body and all comments before adding findings; preserve existing threads and user-authored content. Apply the same existing-feedback check to this draft to make retries idempotent. Reuse it when its `commit_id` matches the reviewed head; report a conflicting pending review instead of replacing another draft. If no new anchored findings remain, create no new review; refresh an existing agent-authored summary only when needed, and report existing feedback links in chat.

   **Complete when:** the PR still matches the reviewed snapshot, every retained finding has passed the refreshed existing-feedback check, and any existing draft is accounted for, or a feedback-fetch failure, revision conflict, or draft conflict is reported.

3. Compose the root `body` using [GitHub review body](review-summary.md#github-review-body), counting each finding once within its axis whether it is new or already raised. If new anchored findings remain and no pending review exists, write a JSON payload containing the pinned `commit_id` and that `body`. Create the draft using:

   ```bash
   gh api --method POST repos/<owner>/<repo>/pulls/<number>/reviews --input <payload.json>
   ```

   Omit `event` to leave the review `PENDING`. Save its REST `id`, GraphQL `node_id`, and URL. For an existing draft, replace the previous agent-authored summary with the current summary, removing superseded assessments while preserving user-authored content. Use `gh api --method PUT repos/<owner>/<repo>/pulls/<number>/reviews/<review-id> --input <payload.json>` with a `body` payload. Keep any still-relevant finding previously stored in the root body in a review thread, or in chat if its file is outside the PR, before replacing that text.

   Add each anchored finding using `gh api graphql` with the `addPullRequestReviewThread` mutation and `pullRequestReviewId` set to that draft's `node_id`. For line threads supply `body`, `path`, `line`, `side`, and, for ranges, `startLine` and `startSide`. For file threads supply `body`, `path`, and `subjectType: FILE`. Store Markdown bodies in JSON files passed with `--input` so newlines, code fences, and shell characters stay literal.

   Keep the review pending for the user to submit. `gh pr review`, review submission endpoints, and standalone comment endpoints are not substitutes for staging draft comments.

   **Complete when:** the root body follows the brief summary format, every new anchored finding is written into the pending review or its failed write is recorded, and findings about files outside the PR remain available for chat.

4. Verify the review using `gh api repos/<owner>/<repo>/pulls/<number>/reviews/<review-id>` and its paginated `/comments` endpoint. Check `PENDING`, the reviewed `commit_id`, the root body's brief summary and counts, and every expected comment's body, path, line/range, or file subject. Recheck PR SHAs and report any movement during posting. Verify that newly saved finding bodies still follow [Comment body](#comment-body). Return the review URL, saved finding count, and links for excluded duplicates in chat; include findings kept in chat and the reason, including any delivery failure.

   **Complete when:** all findings are accounted for in verified saved content, linked existing feedback, findings kept in chat, or explicit failures, and the final report distinguishes pending comments from submitted reviews.

## Check existing feedback

Read all pages of the PR's inline review comments (including replies), submitted review bodies, and conversation comments using `gh api --paginate` on `repos/<owner>/<repo>/pulls/<number>/comments`, `repos/<owner>/<repo>/pulls/<number>/reviews`, and `repos/<owner>/<repo>/issues/<number>/comments`. Include all authors and retain feedback from resolved or outdated threads. Include the authenticated user's visible pending review and its comments; other reviewers' unpublished drafts may be inaccessible, so disclose that limit.

Compare each finding by the affected behavior, triggering condition, and underlying concern, rather than exact wording, line number, review axis, or proposed patch. Exclude feedback that raises the same concern, even if the author proposes a different fix or the thread has moved or resolved. Record the existing comment or review URL and the reason for exclusion. A distinct concern in the same code may remain; explain the difference. Keep the independent axis reports, but stage a shared concern only once when both axes raise it.

**Complete when:** all accessible feedback has been read, every finding is marked new or duplicate with evidence, and any inaccessible feedback or fetch failure is recorded.

## Comment body

Invoke `$spellbinding-sentences` on the exact finding bodies that will be saved after formatting them. Apply the main skill's [finding format](SKILL.md#finding-format) to the explanations and diffs.

Use this order: Conventional Comments opening and discussion, collapsed suggested diff, then the final note: *This feedback was provided by an agent; please confirm the reasoning and suggested change.* Keep the opening, discussion, and note visible outside the collapsed block. Keep titles, headings, severity prefixes, and axis labels outside individual comment bodies; retain axis assessments in the review summary.

Example layout for a hypothetical retry configuration finding:

````markdown
issue (blocking): Setting `options.retries` to `0` still retries the request three times.

`0` should turn retries off.

<details>
<summary>Suggested diff</summary>

```diff
--- a/src/request.ts
+++ b/src/request.ts
@@ -12 +12 @@
-const retries = options.retries || 3;
+const retries = options.retries ?? 3;
```

</details>

*This feedback was provided by an agent; please confirm the reasoning and suggested change.*
````

**Complete when:** each exact body passes the writing workflow and shared finding format, explains the problem and expected behavior in plain language, contains its complete suggested diff in a collapsed block, and ends with the agent confirmation note.

## API references

- [Create and inspect pending reviews](https://docs.github.com/en/rest/pulls/reviews#create-a-review-for-a-pull-request)
- [Pending review threads and their input fields](https://docs.github.com/en/graphql/reference/pulls#addpullrequestreviewthread)
