---
name: parallel-pr-review
description: Review code changes with parallel, fresh-context subagents. Use when reviewing a pull request or preparing a branch for review.
---

# Parallel PR Review

Run an adversarial, read-only review with five independent reviewers. Prefer `/parallel-pr-review <PR#>` to review that GitHub pull request; without a number, review the current branch's PR or its merge base.

## 1. Establish the review target

When given `<PR#>`, run `gh pr view <PR#>` to capture its number, URL, title, body, base and head refs, base and head SHAs, commits, changed files, and discussion. Otherwise identify the current branch's associated PR; if none exists, review the local branch against its merge base. Verify both refs resolve, capture `git diff <merge-base>...<head-sha>`, and stop when the diff is empty. Do not substitute conversation history for repository evidence.

Find the originating plan, spec, or issue plus applicable `AGENTS.md`, `CONTRIBUTING.md`, and relevant ADRs. Record unavailable sources explicitly. Extract the PR's claimed big-picture goal from those sources.

**Complete when:** the immutable review target, exact non-empty diff command, commit list, claimed goal, and available intent and standards sources are known.

## 2. Discover subagents

Call `subagent({ action: "list" })`. Use an executable `reviewer` agent from the result; stop and report the discovery failure if none is available.

**Complete when:** the reviewer runtime name has been verified.

## 3. Launch five reviewers

Call the `subagent` tool once in parallel mode with `async: true`, `context: "fresh"`, `concurrency: 5`, and one task per role below. Reviewers are read-only: they must not modify project/source files or launch subagents.

Every task must tell the reviewer to:

- inspect the exact diff command and immutable base/head SHAs with `git`;
- inspect the associated PR with `gh` when one exists, including its base and discussion relevant to the assigned role;
- read the supplied intent and standards sources relevant to its role;
- infer repository precedent from nearby code and tests;
- do not run build, test, lint, typecheck, or other validation commands; assume they pass and inspect source only;
- report only actionable, evidence-backed findings;
- cite file and line, explain impact, and propose the smallest safe fix;
- return `No findings` when its requirement is satisfied.

Assign exactly one requirement to each reviewer:

1. **Intent conformance:** Check every acceptance criterion in the approved plan or spec against the delivered source. When neither exists, use the user request and PR description. For each claimed goal, trace the changed entry point through its implementation to its intended observable outcome. Flag missing, partial, contradictory, unrequested, or causally unsupported behavior.
2. **Test coverage:** Account for every changed production file. Flag changed behavior without corresponding tests when this repository has precedent for testing that behavior or file area; check changed tests against nearby test structure and helpers.
3. **Code precedent:** Review changed production code against explicit repository standards, nearby style, and shared utilities; flag duplicated local machinery when an established utility already fits.
4. **Correctness:** Find concrete bugs, regressions, unsafe edge cases, and contract violations introduced by the diff.
5. **Design fit:** Check whether the changes follow established repository design patterns. Flag missing patterns only when they prevent a concrete problem; also flag speculative abstractions or pattern overuse.

Use this execution shape, replacing `<reviewer>` and `<target>` with discovered values:

```typescript
subagent({
  tasks: [
    { agent: "<reviewer>", task: "Review immutable diff <diff-command> for intent, acceptance-criteria, goal-to-mechanism evidence, and scope-creep conformance only. ..." },
    { agent: "<reviewer>", task: "Review immutable diff <diff-command> for test coverage and test-file precedent only. ..." },
    { agent: "<reviewer>", task: "Review immutable diff <diff-command> for standards, production-code precedent, and shared utilities only. ..." },
    { agent: "<reviewer>", task: "Review immutable diff <diff-command> for correctness only. ..." },
    { agent: "<reviewer>", task: "Review immutable diff <diff-command> for established design-pattern fit only. ..." }
  ],
  context: "fresh",
  concurrency: 5,
  async: true
})
```

**Complete when:** all five distinct roles are running against the same target.

## 4. Collect and synthesize

Continue any useful parent-side inspection, then call `wait({ all: true })` when no independent work remains. Before synthesis, re-read the PR head SHA; if it moved, discard the reports and restart from target establishment. Inspect failed or incomplete runs with `subagent({ action: "status", id: "..." })`; do not silently omit a role.

Read [`references/TEMPLATE.md`](./references/TEMPLATE.md) before reporting. Deduplicate findings by root cause and reject findings unsupported by the diff or repository precedent. Complete the template in the response:

- state the big-picture goal and a concise, evidence-backed implementation path;
- map each claimed goal to its mechanism, file/line evidence, and whether that causal path is demonstrated;
- ask causal questions only where evidence cannot establish that a mechanism achieves its goal; each must name the goal, mechanism, and missing proof;
- include confirmed findings ordered by severity, dismissed or deferred feedback, all five role results including `No findings`, and unavailable evidence.

Omit inapplicable template sections and placeholders. Do not write a report file unless the user asks. Do not edit code unless the user separately authorizes fixes.

**Complete when:** every role is accounted for, every retained finding is evidence-backed, and every claimed goal is mapped to demonstrated evidence or a precise causal question.
