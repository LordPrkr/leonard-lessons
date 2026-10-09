# GitHub PR review

Use `gh pr view`, `gh pr diff`, and `gh api` for GitHub review work. Resolve the PR URL or number to an explicit host, base repository, and PR number; use the base repository for PR metadata, diffs, and review writes, including fork PRs. For a non-default GitHub host, qualify `--repo` as `<host>/<owner/repo>` and pass `--hostname` to `gh api`.

## Pin the PR

1. Capture PR metadata with `gh pr view <number> --repo <owner/repo> --json url,number,title,body,baseRefOid,headRefOid,headRepository,headRepositoryOwner,commits,closingIssuesReferences`. Fetch linked GitHub issues with `gh issue view` in their owning repositories.

   **Complete when:** the PR identity, base and head SHAs, commit list, description, and linked issue contents are recorded, or a fetch failure is reported.

2. Save `gh pr diff <number> --repo <owner/repo> --color never` as the review diff. Re-read the base and head SHAs after capture; if either changed, recapture metadata and diff. Read supporting source at the pinned revision through `gh api` or an isolated checkout of the PR head. Local `HEAD` is only usable when it matches that revision.

   **Complete when:** the saved diff corresponds to unchanged captured SHAs and is non-empty, or the empty diff or capture failure is reported.

## Stage pending comments

If there are no actionable findings, report that result and skip posting.

1. Follow [Check existing feedback](#check-existing-feedback) and exclude findings already raised by any reviewer. Map each remaining finding to the reviewed PR. Compose bodies using [Comment body](#comment-body); keep axis labels in the review summary. Use the repository-relative `path`, file `line`, and diff `side`: `RIGHT` for added/current lines and `LEFT` for removed lines. For ranges, supply the first line and side as well as the final line and side. Anchor to the smallest relevant range in the saved diff. For a changed file without a suitable line anchor, use a file-level thread; findings about files outside the PR belong in the review body with their file names and proposed diffs.

   For a self-contained replacement of an anchored `RIGHT` range, also include a GitHub `suggestion` fenced block inside the same collapsed block, containing exactly the replacement for that entire range. Broader changes retain their proposed unified diffs.

   **Complete when:** each finding is either excluded with a link to existing feedback or has a valid line or file anchor or review-body placement; every retained body meets the comment format and every suggestion matches its anchored range. If all findings are duplicates, skip writing and report their links.

2. Re-read the PR base and head SHAs before writing. If either moved, refresh the review and revalidate findings and anchors. Refresh the existing-feedback check immediately before writing, excluding any newly raised duplicates. If no new findings remain, skip writing and report the existing feedback links. If the check is incomplete or fails, report the delivery failure and keep findings local until duplicate coverage can be verified. Use `gh api user` and paginated `gh api repos/<owner>/<repo>/pulls/<number>/reviews` to check for the authenticated user's existing `PENDING` review. Read its body and all comments before adding findings; preserve existing content. Apply the same existing-feedback check to this draft to make retries idempotent. Reuse it when its `commit_id` matches the reviewed head; report a conflicting pending review instead of replacing another draft.

   **Complete when:** the PR still matches the reviewed snapshot, every retained finding has passed the refreshed existing-feedback check, and any existing draft is accounted for, or a feedback-fetch failure, revision conflict, or draft conflict is reported.

3. If no pending review exists, write a JSON payload containing the pinned `commit_id` and a `body` with the two-axis summary and any unanchorable findings. Create the draft using:

   ```bash
   gh api --method POST repos/<owner>/<repo>/pulls/<number>/reviews --input <payload.json>
   ```

   Omit `event` to leave the review `PENDING`. Save its REST `id`, GraphQL `node_id`, and URL. For an existing draft, append this run's summary and body findings while preserving prior content, using `gh api --method PUT repos/<owner>/<repo>/pulls/<number>/reviews/<review-id> --input <payload.json>` with a `body` payload.

   Add each anchored finding using `gh api graphql` with the `addPullRequestReviewThread` mutation and `pullRequestReviewId` set to that draft's `node_id`. For line threads supply `body`, `path`, `line`, `side`, and, for ranges, `startLine` and `startSide`. For file threads supply `body`, `path`, and `subjectType: FILE`. Store Markdown bodies in JSON files passed with `--input` so newlines, code fences, and shell characters stay literal.

   Keep the review pending for the user to submit. `gh pr review`, review submission endpoints, and standalone comment endpoints are not substitutes for staging draft comments.

   **Complete when:** every new finding is written into the pending review, or each failed write is recorded with its unsaved comment and proposed diff.

4. Verify the review using `gh api repos/<owner>/<repo>/pulls/<number>/reviews/<review-id>` and its paginated `/comments` endpoint. Check `PENDING`, the reviewed `commit_id`, the review body findings, and every expected comment's body, path, line/range, or file subject. Recheck PR SHAs and report any movement during posting. Verify that newly saved finding bodies still follow [Comment body](#comment-body). Return the review URL, saved finding count, and links for excluded duplicates; include unsaved findings and the failure reason if delivery was partial or blocked.

   **Complete when:** all findings are accounted for in verified saved content or explicit failures, and the final report distinguishes pending comments from submitted reviews.

## Check existing feedback

Read all pages of the PR's inline review comments (including replies), submitted review bodies, and conversation comments using `gh api --paginate` on `repos/<owner>/<repo>/pulls/<number>/comments`, `repos/<owner>/<repo>/pulls/<number>/reviews`, and `repos/<owner>/<repo>/issues/<number>/comments`. Include all authors and retain feedback from resolved or outdated threads. Include the authenticated user's visible pending review and its comments; other reviewers' unpublished drafts may be inaccessible, so disclose that limit.

Compare each finding by the affected behavior, triggering condition, and underlying concern, rather than exact wording, line number, review axis, or proposed patch. Exclude feedback that raises the same concern, even if the author proposes a different fix or the thread has moved or resolved. Record the existing comment or review URL and the reason for exclusion. A distinct concern in the same code may remain; explain the difference. Keep the independent axis reports, but stage a shared concern only once when both axes raise it.

**Complete when:** all accessible feedback has been read, every finding is marked new or duplicate with evidence, and any inaccessible feedback or fetch failure is recorded.

## Comment body

Invoke [/spellbinding-sentences](../spellbinding-sentences/SKILL.md) on the exact bodies that will be saved, including review-body findings, after formatting them. Apply the main skill's [finding format](SKILL.md#finding-format) to the explanations and diffs.

Use this order: explanation, collapsed suggested diff, then the final note: *This feedback was provided by an agent; please confirm the reasoning and suggested change.* Keep the explanation and note visible outside the collapsed block. Give individual comments no title, heading, severity prefix, or axis label; retain axis assessments in the review summary. For review-body findings, use a file-and-line link to locate the concern before the same prose-first body.

Example layout for a hypothetical retry configuration finding:

````markdown
When `options.retries` is `0`, this fallback sets the retry count to `3`. A caller trying to disable retries therefore still sends repeated requests. Please confirm that zero is intended to disable retries; if it is, a nullish fallback preserves that setting while keeping the default for an omitted value.

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

**Complete when:** each exact body passes the writing workflow, explains the current behavior and review check without a title, contains its complete suggested diff in a collapsed block, and ends with the agent confirmation note.

## API references

- [Create and inspect pending reviews](https://docs.github.com/en/rest/pulls/reviews#create-a-review-for-a-pull-request)
- [Pending review threads and their input fields](https://docs.github.com/en/graphql/reference/pulls#addpullrequestreviewthread)
