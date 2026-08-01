---
name: parallel-pr-review
description: Review code changes with parallel, fresh-context subagents. Use when reviewing a pull request or preparing a branch for review.
---

# Parallel PR Review

Run an adversarial, read-only review with five independent reviewers. Follow `/code-brain` for repository identity and evidence, and `/code-brain-writeback` while producing the canonical review artifact. Prefer `/parallel-pr-review <PR#>` to review that GitHub pull request; without a number, review the current branch's PR or its merge base.

## 1. Establish the review target

When given `<PR#>`, run `gh pr view <PR#>` to capture its number, URL, title, body, base and head refs, base and head SHAs, commits, changed files, and discussion. Otherwise identify the current branch's associated PR; if none exists, review the local branch against its merge base. Verify both refs resolve, capture `git diff <merge-base>...<head-sha>`, and stop when the diff is empty. Establish intent from repository, PR, issue, or approved-plan evidence; use conversation history only to locate those sources.

Find the originating plan, spec, or issue plus applicable `AGENTS.md`, `CONTRIBUTING.md`, and relevant ADRs. Record unavailable sources explicitly. Extract the PR's claimed big-picture goal from those sources.

Create `review/pr-<number>-<short-head-sha>-review.md` for a pull request or `review/branch-<short-head-sha>-review.md` for a local branch. Record the immutable target and available intent sources before launching reviewers.

**Complete when:** the immutable review target, exact non-empty diff command, commit list, claimed goal, available intent and standards sources, and review artifact are known.

## 2. Discover subagents

Call `subagent({ action: "list" })`. Use an executable `reviewer` agent from the result; stop and report the discovery failure if none is available.

**Complete when:** the reviewer runtime name has been verified.

## 3. Launch five reviewers

Call the `subagent` tool once in parallel mode with `async: true`, `context: "fresh"`, `concurrency: 5`, and one task per role below. Reviewers are read-only: they must not modify project/source files or launch subagents.

Build one shared task prefix containing the PR number and URL when present, immutable base/head SHAs, exact diff command, claimed goal, intent and standards source paths, and these rules:

- inspect the immutable target with `git` and the associated PR with `gh` when one exists;
- read the supplied intent and standards sources relevant to the assigned role;
- infer repository precedent from nearby code and tests;
- inspect source without running build, test, lint, typecheck, or other validation commands;
- report only actionable, evidence-backed findings;
- cite file and line, explain impact, and propose the smallest safe fix;
- return `No findings` when the role requirement is satisfied;
- keep the review read-only and finish without modifying files or launching subagents.

Append exactly one role requirement below to that complete shared prefix.

Assign exactly one requirement to each reviewer:

1. **Intent conformance:** Check every acceptance criterion in the approved plan or spec against the delivered source. When neither exists, use the user request and PR description. For each claimed goal, trace the changed entry point through its implementation to its intended observable outcome. Flag missing, partial, contradictory, unrequested, or causally unsupported behavior.
2. **Test coverage:** Account for every changed production file. Flag changed behavior without corresponding tests when this repository has precedent for testing that behavior or file area; check changed tests against nearby test structure and helpers.
3. **Code precedent:** Review changed production code against explicit repository standards, nearby style, and shared utilities; flag duplicated local machinery when an established utility already fits.
4. **Correctness:** Find concrete bugs, regressions, unsafe edge cases, and contract violations introduced by the diff.
5. **Design fit:** Check whether the changes follow established repository design patterns. Flag missing patterns only when they prevent a concrete problem; also flag speculative abstractions or pattern overuse.

Use this execution shape after replacing every placeholder:

```typescript
const shared = `Review PR <number-or-none> <url-or-none> at immutable base <base-sha> and head <head-sha>. Diff: <exact-diff-command>. Claimed goal: <goal>. Intent sources: <paths-or-unavailable>. Standards sources: <paths-or-unavailable>. Inspect the target with git and the PR with gh when present; read relevant supplied sources and nearby precedent. Remain read-only, launch no subagents, and run no validation commands. Return only actionable findings with file/line, impact, and smallest safe fix; otherwise return No findings.`

subagent({
  tasks: [
    { agent: "<reviewer>", task: `${shared}\nRole: Intent conformance. <full requirement 1>` },
    { agent: "<reviewer>", task: `${shared}\nRole: Test coverage. <full requirement 2>` },
    { agent: "<reviewer>", task: `${shared}\nRole: Code precedent. <full requirement 3>` },
    { agent: "<reviewer>", task: `${shared}\nRole: Correctness. <full requirement 4>` },
    { agent: "<reviewer>", task: `${shared}\nRole: Design fit. <full requirement 5>` }
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
- include confirmed findings ordered by severity, dismissed or deferred feedback, all five role results including `No findings`, and unavailable evidence;
- record reusable-candidate pointers under `Lessons`.

Omit inapplicable template sections and placeholders. Report the artifact path. Do not edit code unless the user separately authorizes fixes.

**Complete when:** every role is accounted for, every retained finding is evidence-backed, every claimed goal is mapped to demonstrated evidence or a precise causal question, and every reusable lesson is persisted or explicitly absent.
