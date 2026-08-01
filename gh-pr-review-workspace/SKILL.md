---
name: gh-pr-review-workspace
description: Review a GitHub pull request in an isolated cmux workspace. Use when the user provides a PR number and wants the branch checked out into a disposable worktree, its diff opened, parallel review run, selected feedback posted, and cleanup offered.
argument-hint: "<PR#>"
---

# GitHub PR Review Workspace

Accept exactly one pull-request number. Run from any checkout of the target GitHub repository. Use shell-safe quoting for every derived path, ref, and title.

## 1. Pin the repository and PR

From the current checkout, use `gh repo view` to resolve `nameWithOwner` and the repository name. Use `gh pr view <PR#> --repo <nameWithOwner>` to capture the PR URL, title, base ref and OID, head ref and OID, and state. Stop if the PR is not open.

Resolve the shared repository from the invoking checkout with `git rev-parse --path-format=absolute --git-common-dir`. Use the first `worktree` entry from `git worktree list --porcelain` as the source worktree; Git lists the main worktree first. Verify its `gh repo view` identity equals `nameWithOwner`.

Place the disposable worktree beside the source worktree as `<repository-name>-pr-<PR#>-review`; if that path already exists, stop and report it. Use only the invoking repository's Git metadata—cloning or substituting an unrelated checkout is outside this workflow.

**Complete when:** the open PR, immutable base/head OIDs, verified source worktree, and unused disposable path are known.

## 2. Create the review worktree

Stop rather than reuse or overwrite the disposable path.

Fetch the PR into a detached worktree without disturbing the source worktree:

1. Fetch the PR base ref in the source worktree and verify the pinned base OID exists.
2. Run `git worktree add --detach <worktree> <base-oid>` from the source worktree.
3. In the new worktree, run `gh pr checkout <PR#> --repo <nameWithOwner> --detach`.
4. Verify `HEAD` equals the pinned head OID. On setup failure, remove only the worktree created by this run and stop.

The immutable review diff is `git diff <base-oid>...<head-oid>`.

**Complete when:** the disposable worktree is registered, checked out at the pinned PR head, and the exact diff is non-empty.

## 3. Open the cmux review workspace

Create and focus a cmux workspace named `<repository-name> PR #<PR#>` with the worktree as its working directory. Create a new terminal surface (tab) in that workspace, focus it, and use `cmux send` plus `cmux send-key ... Enter` to run the immutable `git diff <base-oid>...<head-oid>` command there. Keep the returned workspace and surface references.

If cmux creation fails, preserve the worktree for diagnosis and report the failure.

**Complete when:** the focused diff tab is running the pinned PR diff in the new workspace.

## 4. Run the parallel review

From the review worktree, invoke `/parallel-pr-review <PR#>` against the pinned base/head OIDs. If the PR head moves, discard the stale result and restart from step 1 with the new OIDs.

After synthesis, number every confirmed finding. Ask which finding numbers, if any, the user wants posted to the PR. For the selected findings, draft one concise review body preserving severity, file/line evidence, impact, and smallest safe fix. Show the exact draft and require confirmation before the external write. Post the confirmed body with:

```bash
gh pr review <PR#> --repo <nameWithOwner> --comment --body-file -
```

Post only the confirmed finding numbers the user explicitly selects; include other material only when the user explicitly requests it.

**Complete when:** all review roles are accounted for and the user has either posted confirmed selected feedback or declined to post feedback.

## 5. Complete cleanup

Beginning with the review result, end every response in this session with one cleanup question while the created worktree exists: `Clean up the review worktree now?`

If the user declines or discusses something else, ask once again at the end of the next response rather than polling. On approval, run `git -C <source-worktree> worktree remove <worktree>` without `--force`. If removal reports changes, show them and ask separately before any forced deletion. Remove only the worktree created by this run.

**Complete when:** the created worktree no longer exists, or the session ends with cleanup still explicitly offered.
