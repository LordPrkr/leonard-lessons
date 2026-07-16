---
name: mystical-tutor
description: "Choose the Leonard Lessons skill that best fits the user's task."
disable-model-invocation: true
---

# Mystical Tutor

Route the request to the narrowest fitting skill. State the chosen route in one sentence, then invoke it. Ask one focused question only when the route depends on missing information.

| Request | Route |
| --- | --- |
| Change code with a tight implementation loop | `/effective-engineer` |
| Make a bounded, approval-first plan | `/pragmatic-plan` |
| Plan or execute broad, risky, or cross-session work | `/code-brain-planning` |
| Initialize, audit, or reconcile Code Brain | `/code-brain` |
| Prove a risky technical path before implementation | `/tracer-bullet` |
| Capture domain terms, bounded contexts, or ADRs | `/domain-modeling` |
| Add diagrams to an existing Code Brain plan | `/code-brain-diagramming` |
| Create or refactor AGENTS.md | `/agents-md` |
| Draft or revise senior-engineer technical writing | `/spellbinding-sentences` |
| Curate Pi sessions into durable memory | `/dreaming` |
| Review a pull request or branch | `/parallel-pr-review` |
| Assess human review comments and plan responses | `/gh-pr-review-plan` |
| Triage failed pull-request jobs | `/gh-pr-job-triage` |

When several routes fit, choose the route matching the user's requested artifact. Use `/effective-engineer` for ordinary code changes and escalate only when durability, approval, or technical uncertainty requires it.

Done when one primary route is selected and invoked, or one blocking routing question is asked.
