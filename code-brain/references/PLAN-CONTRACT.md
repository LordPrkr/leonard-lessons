# Plan Authoring Contract

Use this contract for Code Brain implementation plans. A plan is a standalone handoff for a worker with no prior conversation.

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
