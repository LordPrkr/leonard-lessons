---
name: parallel-pr-review
description: Review code changes with parallel, fresh-context subagents. Use when reviewing a pull request or preparing a branch for review.
---

# Parallel PR Review

Run an adversarial, read-only review with five independent reviewers. Follow `/code-brain` for repository identity and evidence, and `/code-brain-writeback` while producing the canonical review artifact. Prefer `/parallel-pr-review <PR#>` to review that GitHub pull request; without a number, review the current branch's PR or its merge base.

## 1. Establish the review target

When given `<PR#>`, run `gh pr view <PR#>` to capture its number, URL, title, body, base and head refs, base and head SHAs, commits, changed files, and discussion. Otherwise identify the current branch's associated PR; if none exists, review the local branch against its merge base. Verify both refs resolve, capture `git diff <merge-base>...<head-sha>`, and stop when the diff is empty. Establish intent from repository, PR, issue, or approved-plan evidence; use conversation history only to locate those sources.

Find the originating plan, spec, or issue plus applicable `AGENTS.md`, `CONTRIBUTING.md`, and relevant ADRs. From the PR body, issue, commits, and discussion, capture referenced sibling PRs and their stated dependency or landing order. Record unavailable sources explicitly. Extract the PR's claimed big-picture goal from those sources.

Create `review/pr-<number>-<short-head-sha>-review.md` for a pull request or `review/branch-<short-head-sha>-review.md` for a local branch. Record the immutable target and available intent sources before launching reviewers.

**Complete when:** the immutable review target, exact non-empty diff command, commit list, claimed goal, linked-PR dependency evidence, available intent and standards sources, and review artifact are known.

## 2. Discover subagents

Call `subagent({ action: "list" })`. Use an executable `reviewer` agent from the result; stop and report the discovery failure if none is available.

**Complete when:** the reviewer runtime name has been verified.

## 3. Launch five reviewers

Call the `subagent` tool once in parallel mode with `async: true`, `context: "fresh"`, `concurrency: 5`, and one task per role below. Reviewers are read-only: they must not modify project/source files or launch subagents.

Build one shared task prefix containing the PR number and URL when present, immutable base/head SHAs, exact diff command, claimed goal, linked-PR dependency evidence, intent and standards source paths, and these rules:

- inspect the immutable target with `git`, the associated PR with `gh` when one exists, and linked PRs when the assigned role needs their contracts or landing order;
- read the supplied intent and standards sources relevant to the assigned role;
- infer repository precedent from nearby code and tests;
- inspect source without running build, test, lint, typecheck, or other validation commands;
- report only actionable, evidence-backed findings;
- for every feedback item, propose a ready-to-post review comment as a respectful question that invites discussion (for example, “Could we…?” or “Thoughts on…?”), rather than telling the author what to do; explain the impact and a possible safe fix. Give its exact repository-relative filename and line number. Anchor the location to a changed line whenever possible; otherwise identify the nearest relevant line and ensure the comment clearly applies there;
- return `No findings` when the role requirement is satisfied;
- keep the review read-only and finish without modifying files or launching subagents.

Append exactly one role requirement below to that complete shared prefix.

Assign exactly one requirement to each reviewer:

1. **Intent and release safety:** Check every acceptance criterion in the approved plan or spec against the delivered source. When neither exists, use the user request and PR description. For each claimed goal, trace the changed entry point through its intended observable outcome. Read [`references/RELEASE-SAFETY.md`](./references/RELEASE-SAFETY.md); check each relevant linked-PR landing order.
2. **Test proof:** Account for every changed production file. Flag changed behavior without corresponding tests when this repository has precedent for testing that behavior or file area. Read [`references/TEST-PROOF.md`](./references/TEST-PROOF.md) and check changed tests, mocks, stories, fixtures, and helpers against nearby structure and the real contract.
3. **Contract integration and precedent:** Read [`references/CONTRACT-INTEGRATION.md`](./references/CONTRACT-INTEGRATION.md). Trace changed contracts through their boundaries, compare equivalent implementations, and review against explicit standards, nearby style, and shared utilities. Flag duplicated local machinery when an established utility already fits.
4. **State and data correctness:** Read [`references/STATE-DATA-CORRECTNESS.md`](./references/STATE-DATA-CORRECTNESS.md). Find concrete lifecycle, race, cache, pagination, and data-traversal regressions introduced by the diff.
5. **Operational assurance and design fit:** Read [`references/OPERATIONAL-ASSURANCE.md`](./references/OPERATIONAL-ASSURANCE.md) when the diff changes automation, credentials, imports, release artifacts, runbooks, or telemetry. Check established design patterns only when their absence creates a concrete problem; also flag speculative abstractions or pattern overuse.

Use this execution shape after replacing every placeholder:

```typescript
const shared = `Review PR <number-or-none> <url-or-none> at immutable base <base-sha> and head <head-sha>. Diff: <exact-diff-command>. Claimed goal: <goal>. Linked PR dependencies: <evidence-or-none>. Intent sources: <paths-or-unavailable>. Standards sources: <paths-or-unavailable>. Inspect the target with git, the PR with gh when present, and linked PRs when relevant; read relevant supplied sources and nearby precedent. Remain read-only, launch no subagents, and run no validation commands. Return only actionable findings, each with a ready-to-post review comment phrased as a respectful question inviting discussion (such as “Could we…?” or “Thoughts on…?”), exact repository-relative filename and line number, impact, and a possible safe fix; otherwise return No findings.`

subagent({
  tasks: [
    { agent: "<reviewer>", task: `${shared}\nRole: Intent and release safety. <full requirement 1>` },
    { agent: "<reviewer>", task: `${shared}\nRole: Test proof. <full requirement 2>` },
    { agent: "<reviewer>", task: `${shared}\nRole: Contract integration and precedent. <full requirement 3>` },
    { agent: "<reviewer>", task: `${shared}\nRole: State and data correctness. <full requirement 4>` },
    { agent: "<reviewer>", task: `${shared}\nRole: Operational assurance and design fit. <full requirement 5>` }
  ],
  context: "fresh",
  concurrency: 5,
  async: true
})
```

**Complete when:** all five distinct roles are running against the same target.

## 4. Collect and synthesize

Continue any useful parent-side inspection, then call `wait({ all: true })` when no independent work remains. Before synthesis, re-read the PR head SHA; if it moved, discard the reports and restart from target establishment. Inspect failed or incomplete runs with `subagent({ action: "status", id: "..." })` and account for every role in the synthesis.

Read [`references/TEMPLATE.md`](./references/TEMPLATE.md) before reporting. Deduplicate findings by root cause and reject findings unsupported by the diff or repository precedent. Apply `/code-brain-writeback` as each finding is confirmed, dismissed, or deferred. Complete the same template in the review artifact and response:

- state the big-picture goal and a concise, evidence-backed implementation path;
- map each claimed goal to its mechanism, file/line evidence, and whether that causal path is demonstrated;
- ask causal questions only where evidence cannot establish that a mechanism achieves its goal; each must name the goal, mechanism, and missing proof;
- include confirmed findings ordered by severity, dismissed or deferred feedback, all five role results including `No findings`, and unavailable evidence; record exact repository-relative file and line evidence for feedback, and link each posted confirmed finding to its pending inline review comment instead of copying the comment text into the artifact;
- record reusable-candidate pointers under `Lessons`.

Omit inapplicable template sections and placeholders. Report the artifact path. Do not edit code unless the user separately authorizes fixes.

**Complete when:** every role is accounted for, every retained finding is evidence-backed, every claimed goal is mapped to demonstrated evidence or a precise causal question, and every reusable lesson is persisted or explicitly absent.

## 5. Post findings as pending review comments

After synthesis, first inspect this reviewer's existing pending review on the PR. For an earlier review created by this workflow, edit any directive-style AI comments into respectful questions that invite discussion, preserving each finding's substance and evidence; update the root review body to disclose that the thread's comments are AI-generated. Use `PATCH repos/OWNER/REPO/pulls/comments/COMMENT_ID` for inline comment text and `PUT repos/OWNER/REPO/pulls/PR_NUMBER/reviews/REVIEW_ID` for the review body. Leave human-authored comments untouched. Do not duplicate existing feedback. If the earlier review was submitted, edit only this reviewer's own comments when GitHub permits; if an edit fails, report it rather than posting a duplicate.

Post one GitHub pending review containing an inline comment for each confirmed finding. Set the review's root `body` to disclose that its inline comments are AI-generated and need human evaluation, such as: `The inline comments in this review were generated with AI and are offered for human evaluation.` Call `gh api repos/OWNER/REPO/pulls/PR_NUMBER/reviews --method POST --input -` with that `body` and a `comments` array; each comment needs its exact `path`, `line`, `side`, and ready-to-post text phrased as a respectful question inviting discussion, not a directive. Use `RIGHT` for head-side lines and `LEFT` for base-side lines. Omit `event` so GitHub leaves the review pending; do not use `gh pr review --comment`, which submits immediately. Post comments only for confirmed findings, not dismissed feedback or causal questions. If there are no confirmed findings, do not create an empty review.

Use the API response to verify the review is pending and capture each inline comment's `html_url`. Update the artifact to link each confirmed finding to its posted comment rather than duplicating the comment text. If posting or editing fails, the review is not pending, or a comment link is missing, record that precisely in the artifact and report it; never imply that a comment was posted or updated when it was not.

**Complete when:** all earlier workflow comments are phrased as discussion questions, the review root discloses AI authorship, and every confirmed finding has a linked pending inline comment in the artifact—or every failed post/edit is explicitly recorded in both the artifact and response.
