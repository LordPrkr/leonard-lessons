---
name: code-brain-diagramming
disable-model-invocation: true
description: "Add Mermaid diagrams and Obsidian canvases to an existing Code Brain plan."
---

# Code Brain Diagramming

Enrich an existing plan with the smallest set of diagrams that makes its
behavior easier to understand. Use `/code-brain` to resolve the project folder
and plan numbering. Keep every artifact beside the target `plan.md`.

## Steps

### 1. Ground the Diagram

Use the plan named by the user. Without a named plan, list active plans and
continue automatically only when exactly one exists; otherwise ask the user to
choose. Exclude implemented, abandoned, and superseded plans from automatic
selection. Read the selected `plan.md`, linked context notes, and relevant source
files before choosing a diagram.

Done when the target plan exists and every flow, state, ownership boundary, or
comparison to depict is grounded in the plan or source.

### 2. Draw

Create only artifacts that answer a distinct question:

- `call-stack.diagram.md` for runtime execution order
- a descriptive `*.diagram.md` Mermaid file for state, data, or other flows
- `current.canvas` and `proposed.canvas` for a clarifying structural comparison
- a descriptive `*.canvas` for another spatial view

Create Mermaid Markdown or Obsidian Canvas artifacts beside the plan with
`obsidian_create_mermaid` and `obsidian_create_canvas`. Use descriptive
kebab-case names for additional artifacts.

Done when each artifact is legible on its own, matches the grounded evidence,
and contributes information not already clear from another artifact.

### 3. Link

Add one relative Markdown link for every created artifact to `plan.md`,
preserving the plan's existing content and organization.

Done when every created artifact is linked exactly once and every link resolves
from `plan.md`.
