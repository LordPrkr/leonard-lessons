# Leonard Lessons 🪄

Public agent skills from Leonard the Orange 🐦‍🔥

These skills provide a bespoke, local-first Pi + Obsidian workflow. Code Brain stores durable project memory separately from source repositories. Set `CODE_BRAIN_ROOT` to a non-empty vault path or use the default `~/Documents/Code Brain`.

## Main flow

```text
Idea → clarify
       ├─ ordinary implementation → effective-engineer
       ├─ bounded, approval-first work → pragmatic-plan
       ├─ broad work with unresolved decisions → code-brain-wayfinder → code-brain-planning
       ├─ broad, risky, or cross-session work → code-brain-planning
       └─ uncertain technical path → tracer-bullet → return to the plan
Delivery → gh-pr-review-workspace → parallel-pr-review
```

Use `domain-modeling` when clarification settles durable terminology or an architectural decision. Approved bounded plans and durable execution slices each run in a fresh worker with only their plan, never the preceding conversation. If the route is unclear, invoke `mystical-tutor`.

## Code Brain workflow

Code Brain keeps durable project memory outside source repositories. Source code remains the implementation and evidence surface; the vault holds strategic intent, plans, domain language, reusable findings, and execution receipts.

Use Code Brain for work that must survive the current session: broad changes, risky migrations, architectural decisions, or implementation that needs an approval gate. Use `pragmatic-plan` or `effective-engineer` for bounded work that does not need durable artifacts. Ordinary work does not need a Kanban card.

### Project spine

Each initialized project has three entry points:

```text
$CODE_BRAIN_ROOT/<repo>/
├── VISION.md                 # human-owned strategy and agent authority
├── AGENTS.md                 # agent-maintained router to active memory
├── KANBAN.md                 # durable managed-work state
├── plans/<NNN_TOPIC>/        # plan, notes, diagrams, and receipt
├── wayfinding/<NNN_TOPIC>/   # decision maps and tickets
├── todo/                     # durable context for unplanned work
├── domain/                   # glossary, context maps, and ADRs
├── notes/                    # reusable project knowledge
├── resources/                # references and checklists
└── review/                   # ingested review material
```

Run `code-brain` from the target source repository or one of its worktrees. It resolves `<repo>` from Git so every worktree shares one project folder. A bare invocation audits an existing project and offers a concrete reconciliation without changing the vault first. The first durable workflow bootstraps the spine when `VISION.md` is missing: it reads existing repository and vault context, interviews the user one question at a time, and writes `VISION.md` only after explicit confirmation. Projects are reconciled individually, never bulk-migrated.

`VISION.md` defines purpose, principles, non-goals, and what agents may do without asking. `AGENTS.md` links the board, active plans, and canonical notes; it does not hold task state. `KANBAN.md` is a plain-Markdown board rendered by the [Obsidian Kanban plugin](https://github.com/obsidian-community/obsidian-kanban). Install and enable that plugin to use the board UI.

### Durable planning lifecycle

`code-brain-planning` owns the lifecycle for planned work:

```text
Inbox → In Progress → Review → Ready → In Progress → Review → Done
                      approval      implementation

Blocked or partial implementation → receipt → Blocked
```

1. The orchestrator gathers source context and records material claims with repository revisions or external URLs.
2. It writes a numbered `plan.md` with `status: draft`, links it from `AGENTS.md`, and moves its card through drafting and review.
3. Explicit user approval changes the plan to `approved` and moves the card to Ready. Approval does not automatically start implementation.
4. A fresh worker implements the approved plan. Read-only reviewers check correctness, validation, and simplicity.
5. The orchestrator appends an implementation attempt to `receipt.md`, including changed files, verification results, review findings, deviations, and source evidence for every changed repository.
6. Accepted work becomes `implemented` and moves to Done. Blocked, partial, or reverted work keeps its approved design and moves to Blocked with an honest receipt.

Source commits require separate user authorization. Committed work records the delivered commit SHA; uncommitted work records a deterministic hash of the complete Git change set. Plans preserve design intent, Kanban lanes preserve managed-work state, and receipts preserve what actually happened.

### Supporting workflows

- `domain-modeling` promotes stable terms and hard-to-reverse decisions into the glossary or terse ADRs.
- `code-brain-diagramming` keeps Mermaid diagrams and canvases beside the plan they explain.
- `code-brain-wayfinder` turns uncertain, multi-session work into decision tickets tracked on the Code Brain Kanban board before it becomes a plan.
- `tracer-bullet` proves a risky technical path in an isolated worktree and stores only its durable findings.
- `dreaming` deduplicates session transcripts into reviewable memories before promoting high-confidence knowledge.

## Install

List available skills:

```bash
bunx skills add LordPrkr/leonard-lessons --list
```

Install all skills interactively:

```bash
bunx skills add LordPrkr/leonard-lessons
```

Install one skill globally:

```bash
bunx skills add LordPrkr/leonard-lessons --skill effective-engineer --global
```

Install for a specific agent:

```bash
bunx skills add LordPrkr/leonard-lessons --skill effective-engineer --agent claude-code --global
```

## Skills

Dependencies: these workflows require Pi and Obsidian. `gh-pr-review-workspace` requires cmux and `parallel-pr-review`. Install `code-brain` before `code-brain-wayfinder`, `domain-modeling`, `code-brain-diagramming`, `code-brain-planning`, `dreaming`, or `tracer-bullet`. Install `domain-modeling` with `code-brain-planning` or `dreaming` when plans or dreams need glossary or ADR capture. Install the skills you want `mystical-tutor` to route to, or install the full repository.

- `mystical-tutor` — recommend the next Leonard Lessons skill and show where
  it leads without starting the work.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill mystical-tutor --global
  ```

- `code-brain` — canonical project spine, Git-native repository resolution,
  Kanban ownership, and durable evidence conventions.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill code-brain --global
  ```

- `effective-engineer` — tight inspect, red-green implementation, verification,
  and final-review loop for non-trivial code changes.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill effective-engineer --global
  ```

- `code-brain-wayfinder` — chart uncertain, multi-session work as decision
  tickets on the Code Brain Kanban board, then hand the resolved route to
  `code-brain-planning`. Depends on `/code-brain`.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill code-brain --global
  bunx skills add LordPrkr/leonard-lessons --skill code-brain-wayfinder --global
  ```

- `agents-md` — create or refactor AGENTS.md files with progressive
  disclosure: tiny root, linked task-specific guidance, and deletion flags.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill agents-md --global
  ```

- `tracer-bullet` — disposable prototype workflow for proving a plan's
  technical path, then recording findings in Code Brain notes. Depends on
  `/code-brain`.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill code-brain --global
  bunx skills add LordPrkr/leonard-lessons --skill tracer-bullet --global
  ```

- `gh-pr-review-plan` — use `gh` to collect human reviewer PR comments,
  assess them, and plan replies or fixes.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill gh-pr-review-plan --global
  ```

- `gh-pr-job-triage` — classify failed pull-request jobs with parallel,
  evidence-gathering scouts.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill gh-pr-job-triage --global
  ```

- `gh-pr-review-workspace` — check out a numbered GitHub PR into a disposable
  worktree, open its diff in a cmux workspace, run `parallel-pr-review`, post
  selected feedback after confirmation, and keep offering cleanup. Depends on
  `/parallel-pr-review` and the external cmux skill.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill parallel-pr-review --global
  bunx skills add LordPrkr/leonard-lessons --skill gh-pr-review-workspace --global
  ```

- `parallel-pr-review` — review a pull request or branch with five fresh,
  read-only reviewers covering intent, correctness, validation, and design fit.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill parallel-pr-review --global
  ```

- `code-brain-planning` — durable Code Brain planning and execution lifecycle
  for broad, risky, cross-cutting, or approval-first changes, including board
  transitions and implementation receipts. Depends on `/code-brain`; pairs
  with `/domain-modeling` when planning reveals domain terms or ADRs.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill code-brain --global
  bunx skills add LordPrkr/leonard-lessons --skill domain-modeling --global
  bunx skills add LordPrkr/leonard-lessons --skill code-brain-planning --global
  ```

- `code-brain-diagramming` — add Mermaid diagrams and Obsidian canvases to an
  existing Code Brain plan. Depends on `/code-brain`.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill code-brain --global
  bunx skills add LordPrkr/leonard-lessons --skill code-brain-diagramming --global
  ```

- `pragmatic-plan` — lightweight in-session planning with no durable Code
  Brain artifacts and no automatic commit.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill pragmatic-plan --global
  ```

- `spellbinding-sentences` — write technical docs for senior engineers with
  concrete mechanisms, explicit tradeoffs, and plain intent over pedantry.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill spellbinding-sentences --global
  ```

- `domain-modeling` — Code Brain glossary and ADR capture for domain language
  and durable decisions. Depends on `/code-brain`.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill code-brain --global
  bunx skills add LordPrkr/leonard-lessons --skill domain-modeling --global
  ```

- `dreaming` — synthesize local Pi session transcripts into durable Code Brain
  memory. Depends on `/code-brain`; pair with `/domain-modeling` for domain
  terms and ADRs.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill code-brain --global
  bunx skills add LordPrkr/leonard-lessons --skill domain-modeling --global
  bunx skills add LordPrkr/leonard-lessons --skill dreaming --global
  ```

## Other Useful Skills

### [mattpocock/skills](https://github.com/mattpocock/skills)

- `tdd` - test-driven development. Use when the user wants to build features or fix bugs test-first, mentions "red-green-refactor", or wants integration tests.

```
bunx skills@latest add mattpocock/skills/skills/engineering/tdd
```

- `resolving-merge-conflicts` - use when you need to resolve an in-progress git merge/rebase conflict.

```bash
bunx skills@latest add mattpocock/skills/skills/productivity/resolving-merge-conflicts
```

- `grilling` - interview the user relentlessly about a plan or design. Use when the user wants to stress-test a plan before building, or uses any 'grill' trigger phrases.

```
bunx skills@latest add mattpocock/skills/skills/productivity/grilling
```

- `grill-with-docs` - a relentless interview to sharpen a plan or design, which also creates docs (ADR's and glossary) as we go.

```
bunx skills@latest add mattpocock/skills/skills/engineering/grill-with-docs
```

- `writing-great-skills` - reference for writing and editing skills well — the vocabulary and principles that make a skill predictable.

```bash
bunx skills@latest add mattpocock/skills/skills/productivity/writing-great-skills
```

### [cmux](https://cmux.com/docs/skills)

```bash
bunx skills add manaflow-ai/cmux -g -y
```

### [conventional-changelog/skills](https://github.com/conventional-changelog/skills)

- `conventional-commit-message` - generate high-quality Conventional Commit messages.

```bash
bunx skills@latest add conventional-changelog/conventional-changelog/skills/conventional-commit-message
```
