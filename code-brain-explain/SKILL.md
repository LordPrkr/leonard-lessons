---
name: code-brain-explain
description: "Use when a Code Brain plan needs a visual explanation of its problem and proposed solution."
---

# Code Brain Explain

Record a visual explanation of a Code Brain plan's problem and proposed
solution beside it. Use `$code-brain` for project resolution and the
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

Invoke `$show-me` twice, in order:

1. **Problem** — the current behavior and why it falls short, grounded in
   inspected source.
2. **Proposed solution** — the behavior the plan delivers and how it resolves
   the problem.

Done when `$show-me` has illustrated both the problem and the proposed
solution.

### 3. Record the explanation

Write `explanation.md` in the plan's folder with a `## Problem` section and a
`## Proposed solution` section holding the matching illustrations, replacing
any previous version. Save any HTML artifact in the same folder and link it
from its section. Link `explanation.md` from `plan.md`.

Done when `explanation.md` sits beside `plan.md`, illustrates both the problem
and the proposed solution, and is linked from the plan.
