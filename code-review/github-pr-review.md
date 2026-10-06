# GitHub PR review

Use `gh pr view`, `gh pr diff`, and `gh api` for GitHub review work. Resolve the PR URL or number to an explicit host, base repository, and PR number; use the base repository for PR metadata, diffs, and review writes, including fork PRs. For a non-default GitHub host, qualify `--repo` as `<host>/<owner/repo>` and pass `--hostname` to `gh api`.

## Pin the PR

1. Capture PR metadata with `gh pr view <number> --repo <owner/repo> --json url,number,title,body,baseRefOid,headRefOid,headRepository,headRepositoryOwner,commits,closingIssuesReferences`. Fetch linked GitHub issues with `gh issue view` in their owning repositories.

   **Complete when:** the PR identity, base and head SHAs, commit list, description, and linked issue contents are recorded, or a fetch failure is reported.

2. Save `gh pr diff <number> --repo <owner/repo> --color never` as the review diff. Re-read the base and head SHAs after capture; if either changed, recapture metadata and diff. Read supporting source at the pinned revision through `gh api` or an isolated checkout of the PR head. Local `HEAD` is only usable when it matches that revision.

   **Complete when:** the saved diff corresponds to unchanged captured SHAs and is non-empty, or the empty diff or capture failure is reported.

## Stage pending comments

If there are no actionable findings, report that result and skip posting.

1. Map every finding to the reviewed PR. Follow the main skill's [finding format](SKILL.md#finding-format) for comment bodies and retain the Standards or Spec label. Use the repository-relative `path`, file `line`, and diff `side`: `RIGHT` for added/current lines and `LEFT` for removed lines. For ranges, supply the first line and side as well as the final line and side. Anchor to the smallest relevant range in the saved diff. For a changed file without a suitable line anchor, use a file-level thread; findings about files outside the PR belong in the review body with their file names and proposed diffs.

   For a self-contained replacement of an anchored `RIGHT` range, also include a GitHub `suggestion` fenced block containing exactly the replacement for that entire range. Broader changes retain their proposed unified diffs.

   **Complete when:** every finding has a valid line or file anchor, or is assigned to the review body, and every suggestion matches its anchored range.

2. Re-read the PR base and head SHAs before writing. If either moved, refresh the review and revalidate findings and anchors. Use `gh api user` and paginated `gh api repos/<owner>/<repo>/pulls/<number>/reviews` to check for the authenticated user's existing `PENDING` review. Read its body and all comments before adding findings; preserve existing content and skip duplicate findings on retries. Reuse it when its `commit_id` matches the reviewed head; report a conflicting pending review instead of replacing another draft.

   **Complete when:** the PR still matches the reviewed snapshot and any existing draft is accounted for, or a revision or draft conflict is reported.

3. If no pending review exists, write a JSON payload containing the pinned `commit_id` and a `body` with the two-axis summary and any unanchorable findings. Create the draft using:

   ```bash
   gh api --method POST repos/<owner>/<repo>/pulls/<number>/reviews --input <payload.json>
   ```

   Omit `event` to leave the review `PENDING`. Save its REST `id`, GraphQL `node_id`, and URL. For an existing draft, append this run's summary and body findings while preserving prior content, using `gh api --method PUT repos/<owner>/<repo>/pulls/<number>/reviews/<review-id> --input <payload.json>` with a `body` payload.

   Add each anchored finding using `gh api graphql` with the `addPullRequestReviewThread` mutation and `pullRequestReviewId` set to that draft's `node_id`. For line threads supply `body`, `path`, `line`, `side`, and, for ranges, `startLine` and `startSide`. For file threads supply `body`, `path`, and `subjectType: FILE`. Store Markdown bodies in JSON files passed with `--input` so newlines, code fences, and shell characters stay literal.

   Keep the review pending for the user to submit. `gh pr review`, review submission endpoints, and standalone comment endpoints are not substitutes for staging draft comments.

   **Complete when:** every new finding is written into the pending review, or each failed write is recorded with its unsaved comment and proposed diff.

4. Verify the review using `gh api repos/<owner>/<repo>/pulls/<number>/reviews/<review-id>` and its paginated `/comments` endpoint. Check `PENDING`, the reviewed `commit_id`, the review body findings, and every expected comment's body, path, line/range, or file subject. Recheck PR SHAs and report any movement during posting. Return the review URL and saved finding count; include unsaved findings and the failure reason if delivery was partial or blocked.

   **Complete when:** all findings are accounted for in verified saved content or explicit failures, and the final report distinguishes pending comments from submitted reviews.

## API references

- [Create and inspect pending reviews](https://docs.github.com/en/rest/pulls/reviews#create-a-review-for-a-pull-request)
- [Pending review threads and their input fields](https://docs.github.com/en/graphql/reference/pulls#addpullrequestreviewthread)
