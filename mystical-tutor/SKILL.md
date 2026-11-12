---
name: mystical-tutor
description: "Find the Leonard Lessons skill or flow that fits your situation."
disable-model-invocation: true
---

# Mystical Tutor

A tutor finds the next spell; it does not cast it. Recommend the route, then stop.

## Main flow

For work that changes code:

- **Ordinary implementation** → `$effective-engineer`.
- **Work requiring a durable plan and approval first** → `$code-brain-planning`.
- **Settled work needing a scoped tracker project or delivery stories with acceptance criteria and tasks** → `$code-brain-slicing`.
- **Broad work with a clear destination but material unresolved decisions** → `$code-brain-wayfinder`.

Keep bounded work in the current session. Durable planning uses Code Brain and a fresh implementation subagent for each approved plan.

## On-ramps

- **Review a pull request or branch since a fixed point** → `$code-scry`.
- **Assess human review comments and plan responses** → `$gh-pr-review-plan`.
- **Triage failed pull-request jobs** → `$gh-pr-job-triage`.

Use `$gh-pr-review-plan` for reviewer feedback and `$code-scry` for source review since a supplied fixed point.

## Supporting skills

Route directly when the named artifact or discipline is the user's goal:

- **Initialize, audit, or reconcile Code Brain** → `$code-brain`.
- **Explain an existing Code Brain plan visually** → `$code-brain-diagramming`.
- **Create or refactor AGENTS.md** → `$agents-md`.
- **Draft or revise explanatory technical writing** → `$spellbinding-sentences`.
- **Commit, push, and prepare verified work for review** → `$finalize-implementation`.
- **Distill plan or review artifacts into repo-wide documentation** → `$code-brain-distill`.

`$code-brain-diagramming` supports another flow unless its artifact is the requested outcome. `$code-brain` prepares or repairs the workspace; use `$code-brain-planning` for the work itself.

## Answer

Use the request and visible repository context to answer:

```text
Next: `/<skill>`
Why: <request-specific reason>
Then: <next skill or handoff, or "None">
```

Recommend one immediate next skill, even when showing a longer flow. Ask one focused question only when missing information changes that choice. Do not inspect deeply, mutate files, or begin the target skill's work.

Done when one immediate next skill is named, its boundary is clear, the following handoff is stated, and no target work has started.
