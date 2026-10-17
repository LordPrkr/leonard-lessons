# Initialize or Reconcile Code Brain

Use this branch on bare `/code-brain`, when `VISION.md` is missing, or when the user asks to initialize, audit, repair, or reconcile a Code Brain project.

## Reconcile an existing project

Ordinary reads may use legacy projects without changing them. Audit the current project and offer reconciliation; do not mutate the vault until the user confirms the proposed changes.

1. Inspect existing `VISION.md`, `AGENTS.md`, `ISSUE_TRACKER.md` when configured, active plans, historical task notes, and canonical memory.
2. Report missing spine files, broken router links, and plans absent from Active plans.
3. Propose the smallest concrete repair; ask the user about ambiguous work.
4. After confirmation, repair navigation without rewriting durable content or bulk-migrating unrelated projects.

Done when the user has declined changes or confirmed a project whose spine resolves and active-plan links are current.

## Bootstrap a project

When durable planning targets a project without `VISION.md`:

1. Read existing Code Brain artifacts and the source repository's README, AGENTS files, and relevant docs.
2. Interview the user one question at a time until Purpose, Agent authority, and Non-goals are explicit.
3. Obtain explicit confirmation of `VISION.md`.
4. Read [`PROJECT_SPINE.md`](./PROJECT_SPINE.md) and its [filled `AGENTS.md` example](./EXAMPLE_AGENTS.md), then write `VISION.md` and `AGENTS.md` from the templates, omitting links to notes that do not exist.
5. Resume the calling workflow.

Do not invent strategic intent or bulk-bootstrap legacy projects.

Done when `VISION.md` and `AGENTS.md` exist, the user confirmed `VISION.md`, and every `AGENTS.md` router link resolves.
