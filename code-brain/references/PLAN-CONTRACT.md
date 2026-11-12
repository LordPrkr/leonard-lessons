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

Set `date` once when creating the plan. Use `draft`, `approved`, `implemented`, `abandoned`, or `superseded` for `status`: explicit user approval sets `approved`; a substantive design revision to a `draft` or `approved` plan restores `draft` and requires approval again; completed, verified delivery sets `implemented`; an explicit decision to stop sets `abandoned`; and a replacement plan sets `superseded`. An implementation attempt that is blocked, partial, reverted, or not finalized remains `approved`.

`implemented` is immutable: after setting that status, preserve the entire plan unchanged. Capture later corrections, outcomes, or changed design in a new artifact; a changed implementation requires a new plan.

Read legacy `approved:` through `$code-brain`'s compatibility mapping, but never write it.

## Plan sections

Use these sections in order: Problem, Goal, Precedent, and Scope. The calling workflow may add an Outcome linking the delivery receipt. Apply `$spellbinding-sentences` to the explanatory prose.

- **Problem:** one or two concise sentences about the problem.
- **Goal:** one or two concise sentences about the desired outcome.
- **Precedent:** briefly summarize applicable patterns with references to repository paths and definitions. Omit source revisions.
- **Scope:** a short list of the affected packages or package subdirectories, each with a one-line summary of what changes there. Stay at package level; the implementation subagent chooses files and definitions.

```md
- `libs/runner` — accept a caller-selected policy for each operation.
- `apps/cli/src/commands` — expose the policy as a flag.
```

Present the current design without superseded alternatives.

## Completion

The plan is ready for approval when a fresh implementation subagent can understand the problem, goal, precedent to follow, and affected scope without the preceding conversation.
