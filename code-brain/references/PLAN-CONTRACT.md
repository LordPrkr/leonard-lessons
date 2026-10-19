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

Read legacy `approved:` through `$code-brain`'s compatibility mapping, but never write it.

## Plan sections

Use these sections in order: Problem, Goal, Context, Precedent, Deviations, Files, Implementation, Test Strategy, and Questions. The calling workflow may add an Outcome linking the delivery receipt. Apply `$spellbinding-sentences` to the explanatory prose.

- **Problem:** one or two concise sentences about the problem.
- **Goal:** one or two concise sentences about the desired outcome.
- **Context:** one or two concise sentences summarizing the user's specific ask.
- **Precedent:** briefly summarize applicable patterns with references to repository paths and definitions. Omit source revisions.
- **Deviations:** record necessary departures and their authorization or requested decisions using `$follow-precedent`'s disclosure fields, including conflicts and search gaps.

Resolve implementation choices before approval; keep unanswered decisions visible in Questions. Present the current design without superseded alternatives.

## Files

Show a high-level tree of the repository-relative files expected to change in a fenced `text` block. Prefix each affected file with `M` for modified, `A` for added, or `D` for deleted. Include test files here when they are expected to change. Label repository roots when several repositories are affected.

```text
src/
M ├── service.ts
A ├── policy.ts
D └── legacy.ts
tests/
M └── service.test.ts
```

## Implementation

Organize the overview by behavior change, with a descriptive heading for each
entry. Name the repository-relative paths and affected definitions once per
entry; for configuration or prose, identify the relevant keys or headings.

For changed behavior, use concise **Before** and **After** statements. For
additions or deletions, use **Add** or **Remove** and explain the reason. Add
**Why** when the motivation is not already clear. Include exact signatures or
small code excerpts only when their syntax matters to the design. Keep
test-file changes in Test Strategy.

### Apply the selected policy

`src/runner.ts` — `run`

- **Before:** Always use the default policy.
- **After:** Accept the caller's selected policy and apply it before running
  the operation.
- **Why:** Callers need to choose a policy for each operation.

Diagrams supplement these entries; preserve the implementation choices a
fresh agent needs even when the diagram omits them for readability.

## Test Strategy

Summarize how each proposed change will be checked, following the closest existing tests, fixtures, and commands. Name the behavior and test seam or manual check; include commands only when they help carry out the check.

When a change does not deserve an automated test, say so with a short reason. Examples include tautological checks of constants or styles, or a new test that would depart from repository precedent without a concrete coverage need. Use a proportionate existing check or manual inspection instead.

## Questions

List open questions, or write `None.` As answers arrive in chat, strike through the original question and record its answer on the same item:

- ~~Should the operation retry?~~ Answer: No; preserve the existing single-attempt behavior.

Apply each answer to the affected plan sections. A question is resolved only when its answer is documented and the plan agrees with it.

## Completion

The plan is ready for review when a fresh implementation subagent can identify the intended file and definition changes, each change has a proportionate test strategy or a reason for omitting tests, and unanswered questions are explicit.
