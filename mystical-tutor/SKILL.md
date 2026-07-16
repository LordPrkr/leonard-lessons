---
name: mystical-tutor
description: "Find the Leonard Lessons skill or flow that fits your situation."
disable-model-invocation: true
---

# Mystical Tutor

A tutor finds the next spell; it does not cast it. Recommend the route, then stop.

## Main flow

For work that changes code:

- **Ordinary implementation** → `/effective-engineer`.
- **Bounded work requiring a plan and approval first** → `/pragmatic-plan`.
- **Broad, risky, cross-cutting, or cross-session work** → `/code-brain-planning`.

Keep bounded work in the current session. Durable planning uses Code Brain and fresh workers for context-sized execution slices.

## Detour

When a plan depends on a technical question that conversation cannot answer, route to `/tracer-bullet`. Its runnable evidence returns to the plan; the prototype is not the deliverable.

## On-ramps

- **Review a pull request or branch** → `/parallel-pr-review`.
- **Assess human review comments and plan responses** → `/gh-pr-review-plan`.
- **Triage failed pull-request jobs** → `/gh-pr-job-triage`.

Do not substitute `/gh-pr-review-plan` for code review or `/parallel-pr-review` for assessing reviewer feedback.

## Supporting skills

Route directly when the named artifact or discipline is the user's goal:

- **Initialize, audit, or reconcile Code Brain** → `/code-brain`.
- **Capture domain terms, bounded contexts, or ADRs** → `/domain-modeling`.
- **Add diagrams to an existing Code Brain plan** → `/code-brain-diagramming`.
- **Create or refactor AGENTS.md** → `/agents-md`.
- **Draft or revise senior-engineer technical writing** → `/spellbinding-sentences`.
- **Curate Pi sessions into durable memory** → `/dreaming`.

`/domain-modeling` and `/code-brain-diagramming` support another flow unless their artifact is the requested outcome. `/code-brain` prepares or repairs the workspace; use `/code-brain-planning` for the work itself.

## Answer

Use the request and visible repository context to answer:

```text
Next: `/<skill>`
Why: <request-specific reason>
Then: <next skill or handoff, or "None">
```

Recommend one immediate next skill, even when showing a longer flow. Ask one focused question only when missing information changes that choice. Do not inspect deeply, mutate files, or begin the target skill's work.

Done when one immediate next skill is named, its boundary is clear, the following handoff is stated, and no target work has started.
