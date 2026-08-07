# Plan Authoring Contract

Use this contract for Code Brain implementation plans. A plan is a standalone handoff for a worker with no prior conversation.

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

## Required content

State the problem, goal, out-of-scope boundary, relevant context, observable acceptance criteria, exact repository-relative files, the highest existing public test seam, tests, verification commands, risks, blocking questions, and artifact links. Apply `/spellbinding-sentences` to the plan's explanatory prose.

Give each observable behavior one red-green implementation step. Resolve implementation branches before approval; record any unresolved choice as a blocking question. Present the current plan without superseded alternatives.

## Implementation diffs

Every code-changing step names each affected repository-relative path and immediately shows a fenced unified diff. Diffs express human-reviewed design intent; acceptance criteria govern delivery, and workers report evidence-backed implementation deviations.

Include enough unchanged context and `-`/`+` lines to distinguish current code from the proposed change. Mark new and deleted files with `/dev/null`, include the full contents of a small new file, and use enough path-labeled diffs to show how connected changes fit together.

````md
**`src/example.ts`**

```diff
-export const example = "current"
+export const example = "proposed"
```
````

## Completion

The plan is ready for review when a fresh worker can execute it, every acceptance criterion maps to implementation and verification, every code-changing step has path-labeled before-and-after diffs, and no unresolved choice is hidden in conditional prose.
