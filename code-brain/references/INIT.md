# Initialize or Reconcile Code Brain

Use this branch when `VISION.md` is missing or the user asks to initialize, audit, repair, or reconcile a Code Brain project.

## Reconcile an existing project

Ordinary reads may use legacy projects without changing them. Audit the current project and offer reconciliation; do not mutate the vault until the user confirms the proposed changes.

1. Inspect existing `VISION.md`, `AGENTS.md`, `KANBAN.md`, active plans, todo notes, and canonical memory.
2. Report missing spine files, broken router links, plans absent from Active plans, duplicate board cards, and one-line todo notes that should be inline cards.
3. Propose the smallest concrete repair. Never infer a Kanban lane from plan age or design status; ask the user about ambiguous work.
4. After confirmation, repair navigation and selected cards without rewriting durable content or bulk-migrating unrelated projects.

Done when the user has declined changes or confirmed a project whose spine resolves, active-plan links are current, and each selected managed task appears in one lane.

## Bootstrap a project

When durable planning targets a project without `VISION.md`:

1. Read existing Code Brain artifacts and the source repository's README, AGENTS files, and relevant docs.
2. Interview the user one question at a time until Purpose, Agent authority, and Non-goals are explicit.
3. Obtain explicit confirmation of `VISION.md`.
4. Read [`PROJECT_SPINE.md`](./PROJECT_SPINE.md) and its [filled `AGENTS.md` example](./EXAMPLE_AGENTS.md), then write all three project files from the templates, omitting links to notes that do not exist.
5. Resume the calling workflow.

Do not invent strategic intent or bulk-bootstrap legacy projects.

Done when all three project files exist, the user confirmed `VISION.md`, every `AGENTS.md` router link resolves, and `KANBAN.md` contains all six initialized lanes.
