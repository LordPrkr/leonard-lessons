# Plan Authoring Contract

Use this contract for Code Brain implementation plans. A plan is a standalone handoff for an implementation subagent with no prior conversation.

## Frontmatter and status

Every plan starts with the same frontmatter:

```yaml
---
date: YYYY-MM-DD
status: draft
---
```

Set `date` once when creating the plan. Use `draft`, `approved`, `implemented`, `abandoned`, or `superseded` for `status`: explicit user approval sets `approved`; a substantive design revision to a `draft` or `approved` plan restores `draft` and requires review plus approval; completed, verified delivery sets `implemented`; an explicit decision to stop sets `abandoned`; and a replacement plan sets `superseded`. An implementation attempt that is blocked, partial, reverted, or not finalized remains `approved`.

`implemented` is immutable: after setting that status, preserve the entire plan unchanged. Capture later corrections, outcomes, or changed design in a new artifact; a changed implementation requires a new plan.

Read legacy `approved:` through `/code-brain`'s compatibility mapping, but never write it.

## Plan sections

Use these sections in order: Problem, Goal, Context, Precedent, Deviations, Files, Implementation, Test Strategy, and Questions. The calling workflow may add an Outcome linking the delivery receipt. Apply `/spellbinding-sentences` to the explanatory prose.

- **Problem:** one or two concise sentences about the problem.
- **Goal:** one or two concise sentences about the desired outcome.
- **Context:** one or two concise sentences summarizing the user's specific ask.
- **Precedent** and **Deviations:** the applicable patterns, source revisions, and authorized or requested departures required by `/follow-precedent`. Cite evidence beside the claim it supports and link sibling artifacts where relevant.

Resolve implementation choices before approval; keep unanswered decisions visible in Questions. Present the current design without superseded alternatives.

## Files

Show a high-level tree of the repository-relative files expected to change in a fenced `diff` block. Prefix each affected file with `+` for add, `-` for delete, or `/` for change. Include test files here when they are expected to change. Label repository roots when several repositories are affected.

```diff
 src/
/├── service.ts
+├── policy.ts
-└── legacy.ts
 tests/
/└── service.test.ts
```

## Implementation

Group the overview by top-level definitions being **Added**, **Changed**, and **Deleted**, using fenced `diff` blocks. Put a concise comment immediately above each definition's signature or name explaining the intended behavior and why it is needed. Use `+` for additions, `-` for deletions, and paired old/new lines for changes; omit empty groups.

Show signatures or names only, without fleshed-out bodies or per-file patches. Qualify names only as needed to locate them. For configuration or prose, use top-level keys or headings as the definitions. Keep test-file changes in Test Strategy.

### Added

```diff
+// Choose the applicable policy so callers share one decision rule.
+export function selectPolicy(input: Input): Policy
```

### Changed

```diff
-// Always use the default policy.
-export function run(input: Input): Result
+// Apply the selected policy before running the operation.
+export function run(input: Input, policy: Policy): Result
```

### Deleted

```diff
-// Remove the obsolete entry point now that run handles policy selection.
-export function runLegacy(input: Input): Result
```

## Test Strategy

Summarize how each proposed change will be checked, following the closest existing tests, fixtures, and commands. Name the behavior and test seam or manual check; include commands only when they help carry out the check.

When a change does not deserve an automated test, say so with a short reason. Examples include tautological checks of constants or styles, or a new test that would depart from repository precedent without a concrete coverage need. Use a proportionate existing check or manual inspection instead.

## Questions

List open questions, or write `None.` As answers arrive in chat, strike through the original question and record its answer on the same item:

- ~~Should the operation retry?~~ Answer: No; preserve the existing single-attempt behavior.

Apply each answer to the affected plan sections. A question is resolved only when its answer is documented and the plan agrees with it.

## Completion

The plan is ready for review when a fresh implementation subagent can identify the intended file and definition changes, each change has a proportionate test strategy or a reason for omitting tests, and every blocking question has a documented answer reflected in the design.
