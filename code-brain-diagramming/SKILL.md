---
name: code-brain-diagramming
description: "Use when a Code Brain plan needs a visual explanation of behavior changes, execution order, states, or dependencies."
---

# Code Brain Diagramming

Record a visual explanation of a Code Brain plan beside it. Use `$code-brain`
for project resolution and the
[plan authoring contract](../code-brain/references/PLAN-CONTRACT.md) for
revisions and approval status.

## Steps

### 1. Ground the explanation

Use the plan supplied by the user or calling workflow. Without a named plan,
list active plans and continue automatically only when exactly one exists;
otherwise ask the user to choose. Exclude implemented, abandoned, and superseded
plans from automatic selection. Read the selected `plan.md`, linked context
notes, and relevant source files.

Distinguish observed current behavior from proposed behavior; raise unresolved
design choices with the user instead of depicting them.

Done when the target plan is unambiguous and every behavior or relationship to
depict is supported by the plan or inspected source.

### 2. Invoke show-me

Invoke `$show-me` with the plan as the current topic.

Done when `$show-me` has produced its explanation of the plan.

### 3. Record the explanation

Write the explanation to `explanation.md` in the plan's folder, replacing any
previous version. Save any HTML artifact in the same folder and link it from
`explanation.md`. Link `explanation.md` from `plan.md`.

Done when `explanation.md` sits beside `plan.md`, contains the complete
explanation, and is linked from the plan.
