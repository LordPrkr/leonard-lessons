---
name: code-review
description: "Use when reviewing a GitHub PR, a branch, or committed changes since a commit, tag, or merge-base. Enforces applicable precedent through independent Standards and Spec reviews, proposes diffs, and stages pending inline comments for GitHub PRs through gh."
---

**Follow precedent.** Invoke [/follow-precedent](../follow-precedent/SKILL.md) before reviewing. Existing implementation and test patterns are enforceable Standards sources even when no prose standard documents them.

Two-axis review of a GitHub PR or the diff between `HEAD` and a fixed point the user supplies:

- **Standards**: does the code conform to applicable precedent and documented repository standards, with every departure justified and authorized?
- **Spec**: does the code faithfully implement the originating issue / spec?

Both axes run as **parallel sub-agents** so they don't pollute each other's context, then this skill aggregates their findings.

## Process

### 1. Pin the review scope

For a GitHub PR, use `gh` and follow [GitHub PR review — Pin the PR](github-pr-review.md#pin-the-pr). The PR supplies the comparison; a separate fixed point is unnecessary.

For a local review, use the supplied fixed point (a commit SHA, branch name, tag, `main`, `HEAD~5`, etc.). If neither a PR nor a fixed point is specified, ask for the review target. Capture the diff command once: `git diff <fixed-point>...HEAD` (three-dot, so the comparison is against the merge-base). Also note the list of commits via `git log <fixed-point>..HEAD --oneline`.

Before delegation, confirm local refs resolve (`git rev-parse <fixed-point>` and `git rev-parse HEAD`) or the PR snapshot is pinned, and the diff is non-empty. Record both local SHAs so reviewers use the same revisions even if the branch moves. Local comparisons cover committed changes.

**Complete when:** the target, pinned revisions, exact non-empty diff or saved PR diff, and commit list are captured, or a resolution failure or empty diff has been reported before delegation.

### 2. Identify the spec source

For a PR, start with its captured description and linked issues. Look for any remaining originating spec, in this order:

1. Issue references in the commit messages (`#123`, `Closes #45`, GitLab `!67`, etc.), fetched with the repository’s available issue-tracker tooling. Follow `docs/agents/issue-tracker.md` when that file exists.
2. A path the user passed as an argument.
3. A spec file under `docs/`, `specs/`, or `.scratch/` matching the branch name or feature.
4. If nothing is found, ask the user where the spec is. If they say there isn't one, the **Spec** sub-agent will skip and report "no spec available".

**Complete when:** the spec path or fetched contents are available, or the user has confirmed there is no spec and the Spec axis will be skipped.

### 3. Identify the standards and precedent sources

Read guidance at the pinned review revision that documents how code should be written, such as `CODING_STANDARDS.md` or `CONTRIBUTING.md`.

Locate the closest applicable implementations, callers, and tests in the pre-change source at the pinned merge-base or PR diff base. Record paths, symbols, revisions, and why each example applies. Capture disclosed deviations and their task or approval evidence. The Standards reviewer must verify applicability and search gaps across the full diff; code introduced by the reviewed change cannot establish its own precedent.

On top of these sources, the Standards axis carries the **smell baseline** below: a fixed set of Fowler code smells (_Refactoring_, ch.3). Two rules bind it:

- **Standards and precedent override smells.** Suppress a smell recommendation that conflicts with an applicable documented rule, applicable precedent, or an explicitly authorized task requirement. A general refactoring preference cannot justify a departure.
- **Always a judgement call.** Each smell is a labelled heuristic ("possible Feature Envy"), never a hard violation. Like any standard here, skip anything tooling already enforces.

Each smell reads *what it is* → *how to fix*; match it against the diff:

- **Mysterious Name**: a function, variable, or type whose name doesn't reveal what it does or holds. → rename it; if no honest name comes, the design's murky.
- **Duplicated Code**: the same logic shape appears in more than one hunk or file in the change. → extract the shared shape, call it from both.
- **Feature Envy**: a method that reaches into another object's data more than its own. → move the method onto the data it envies.
- **Data Clumps**: the same few fields or params keep travelling together (a type wanting to be born). → bundle them into one type, pass that.
- **Primitive Obsession**: a primitive or string standing in for a domain concept that deserves its own type. → give the concept its own small type.
- **Repeated Switches**: the same `switch`/`if`-cascade on the same type recurs across the change. → replace with polymorphism, or one map both sites share.
- **Shotgun Surgery**: one logical change forces scattered edits across many files in the diff. → gather what changes together into one module.
- **Divergent Change**: one file or module is edited for several unrelated reasons. → split so each module changes for one reason.
- **Speculative Generality**: abstraction, parameters, or hooks added for needs the spec doesn't have. → delete it; inline back until a real need shows.
- **Message Chains**: long `a.b().c().d()` navigation the caller shouldn't depend on. → hide the walk behind one method on the first object.
- **Middle Man**: a class or function that mostly just delegates onward. → cut it, call the real target direct.
- **Refused Bequest**: a subclass or implementer that ignores or overrides most of what it inherits. → drop the inheritance, use composition.

**Complete when:** documented standards and candidate precedent sources are listed with pinned references, any search gaps or conflicts are explicit, disclosed deviations have authorization evidence or an explicit gap, and the shared contract and smell baseline are ready to include in the Standards prompt.

### 4. Spawn both sub-agents in parallel

Give both sub-agents the pinned review scope from step 1 and paste the full Follow precedent contract and [finding format](#finding-format) below into their prompts. For a PR, pass the saved diff and PR metadata rather than a command against local `HEAD`. Each brief's word limit applies to prose; proposed diffs are additional.

**Standards sub-agent prompt** should include:

- The saved diff or full diff command using pinned SHAs, and the commit list.
- The standards and precedent sources, pinned pre-change revision, disclosed deviations, and authorization evidence from step 3, **plus the smell baseline** pasted into the prompt (the sub-agent has no other access to it).
- The brief: "Apply Follow precedent to every substantive implementation, validation, and test choice in the pinned diff, including the affected module's test conventions. Report every documented-standard violation with its source and rule. For each unjustified or unauthorized pattern departure, cite the pre-change path and symbol, explain applicability, identify the difference, and propose the smallest correction. Verify authorization against the task or an approved decision. Demonstrated pattern breaches are Standards violations even without a written rule. Report baseline smells as judgement calls subject to the precedence rules. Apply the shared contract to proposed fixes too. Skip anything tooling enforces. Return all findings, precedent coverage, and inspection limits; keep prose concise without truncating findings to meet a word budget."

**Spec sub-agent prompt** should include:

- The saved diff or diff command using pinned SHAs, and the commit list.
- The path or fetched contents of the spec.
- The brief: "Report: (a) requirements the spec asked for that are missing or partial; (b) behaviour in the diff that wasn't asked for (scope creep); (c) requirements that look implemented but where the implementation looks wrong. Quote the spec line for each finding. Under 400 words."

If the spec is missing, skip the Spec sub-agent and note this in the final report.

**Complete when:** every applicable axis has returned its report from a separate sub-agent, or a failed run is explicitly reported; Standards accounts for the full diff against precedent or names inspection limits; a missing spec is recorded as a skipped Spec axis.

### 5. Aggregate

Invoke [/spellbinding-sentences](../spellbinding-sentences/SKILL.md) and apply its writing workflow to each finding's explanation. Check each actionable finding against the [finding format](#finding-format), completing any missing proposed diff from the pinned source. Verify that each proposed correction follows cited precedent or an authorized deviation. Standards owns completion of the complete-diff audit required by Follow precedent. Preserve the evidence, uncertainty, and proposed correction while revising the prose. Prepare the two reports under `## Standards` and `## Spec` headings. Do **not** merge or rerank findings, because the two axes are deliberately separate (see _Why two axes_).

Inspect the pinned diff and supporting source for the [manual review priorities](review-summary.md#manual-review-priorities), including changes with no Standards or Spec findings. Trace affected contracts, consumers, database operations, and request call sites far enough to explain their consequences. Record changed, unchanged, or unverified status for every applicable category, with source evidence for each changed area.

Record each axis's finding count and worst issue, or its skip or failure. Include the precedent sources checked, authorized deviations, and unresolved gaps or conflicts in Standards coverage. Keep these assessments separate; inspection limits preclude a claim of full precedent conformance.

**Complete when:** every actionable finding and proposed fix satisfies the finding format and shared precedent contract, Standards and Spec reports are ready separately with their counts and assessments, and precedent coverage and every applicable manual review category are accounted for with evidence or an explicit inspection limit.

### 6. Stage GitHub PR comments

For a GitHub PR, follow [GitHub PR review — Stage pending comments](github-pr-review.md#stage-pending-comments) with the completed findings. Capture the pending review link and delivery status for the final response. For local reviews, skip posting.

**Complete when:** every PR finding is accounted for in a verified pending review, a linked duplicate already raised by a reviewer, or an explicit delivery failure, or there are no actionable PR findings or the review is local and posting is skipped.

### 7. Deliver the review overview and manual review guide

Apply [/spellbinding-sentences](../spellbinding-sentences/SKILL.md) to the whole final response and follow the [review summary format](review-summary.md#final-response). Use the evidence from step 5 and delivery status from step 6. Deliver this response even when both axes have no findings.

**Complete when:** the user has received an overview of what the change accomplishes, a manual review guide with source snippets and concrete checks for every changed priority area, explicit coverage limits, the separate Standards and Spec reports, and any GitHub delivery status.

## Finding format

Every actionable finding, on either axis and for every review target, includes:

- The affected repository-relative file path and line or range when present in the reviewed revision.
- An explanation that leads with the code's current state or behavior under a concrete condition and its consequence for users or maintainers. Explain why that behavior needs further review and name the concrete condition or check the reviewer should confirm. Then describe the intended state or behavior according to the review and how the proposed change closes that gap. Support the recommendation with the cited standard, applicable precedent, baseline smell, or spec requirement; a smell label alone is insufficient. For a precedent violation, cite the pre-change path and symbol, explain its applicability, and identify the unjustified departure. Keep the explanation proportional to the issue, with enough context for the author to understand why the change matters and decide what to do.
- A concrete proposed unified diff inside a collapsed `<details>` block with `<summary>Suggested diff</summary>` and a blank line before the `diff` fence and before `</details>`. The diff uses `--- a/<path>` and `+++ b/<path>` file headers and hunk ranges. Include every file needed for the correction; use `/dev/null` for added or deleted files. Show replacement code rather than placeholders such as “fix this here.”

Keep proposals consistent with the pinned source and label any unverified assumptions or validation limits. Propose changes for the user to assess; applying them is separate work. If an axis has no findings, say so without inventing a diff.

## Why two axes

A change can pass one axis and fail the other:

- Code that follows every standard but implements the wrong thing → **Standards pass, Spec fail.**
- Code that does exactly what the issue asked but breaks the project's conventions → **Spec pass, Standards fail.**

Reporting them separately stops one axis from masking the other.
