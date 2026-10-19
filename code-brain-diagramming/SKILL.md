---
name: code-brain-diagramming
description: "Use when a Code Brain plan needs an inline Mermaid diagram to clarify behavior changes, execution order, states, or dependencies."
---

# Code Brain Diagramming

Make a Code Brain plan skimmable with the smallest set of inline Mermaid
diagrams that explains its behavior. Use `$code-brain` for project resolution
and the [plan authoring contract](../code-brain/references/PLAN-CONTRACT.md)
for revisions and approval status.

## Steps

### 1. Ground the diagram

Use the plan supplied by the user or calling workflow. Without a named plan,
list active plans and continue automatically only when exactly one exists;
otherwise ask the user to choose. Exclude implemented, abandoned, and superseded
plans from automatic selection. Read the selected `plan.md`, linked context
notes, and relevant source files before choosing a diagram.

Distinguish observed current behavior from proposed behavior; keep unresolved
design choices visible in the plan's Questions.

Done when the target plan is unambiguous and every behavior or relationship to
depict is supported by the plan or inspected source.

### 2. Choose the view

Choose a diagram only when it answers a question more clearly than prose:

- Use a flowchart for routing, data flow, ownership, or dependencies.
- Use a sequence diagram when interactions and execution order matter.
- Use a state diagram when allowed transitions are the subject.
- For behavior changes, use a before-and-after view following
  [the comparison example](./references/COMPARISON.md).

Group by behavior rather than file. Give each diagram a descriptive heading
and one question to answer; keep independent changes in separate views. Leave
simple edits as prose when a diagram would only repeat the change entry.

Done when every selected view has a distinct purpose and changes that need
only prose remain understandable without a diagram.

### 3. Draw inline

Write fenced `mermaid` blocks directly in `plan.md`, beside the behavior they
explain. Use short, concrete node labels and label edges when their condition
or meaning would otherwise be unclear. State the intended outcome in a short
caption. Put repository-relative paths and affected definitions immediately
below the diagram so implementation details do not crowd the nodes.

Prefer top-to-bottom flows at ordinary document width. Keep each view small
enough to scan without zooming; split dense diagrams by behavior. Use text
labels to distinguish current, proposed, added, or removed behavior so meaning
does not depend on color.

Done when every diagram is inline, readable on its own, and accompanied by
enough location detail for a fresh implementation agent to find the change.

### 4. Verify

Check every node, edge, condition, and omission against the grounded evidence.
Ensure diagrams and change entries agree and preserve the plan's unrelated
content. Render with an available Mermaid preview or validator and inspect
labels, layout, and syntax; report the limitation if no renderer is available.
Apply the linked plan contract when the revision changes the approved design.

Done when every diagram matches the plan and source, rendering has been checked
or its absence reported, and the plan's status reflects any design revision.
