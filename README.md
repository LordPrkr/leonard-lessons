# Leonard Lessons 🪄

Public agent skills from Leonard the Orange 🐦‍🔥

These skills provide a bespoke, local-first Pi + Obsidian workflow. Code Brain stores durable project memory separately from source repositories. Set `CODE_BRAIN_ROOT` to a non-empty vault path or use the default `~/Documents/Code Brain`.

## Main flow

```text
Idea → clarify
       ├─ ordinary implementation → effective-engineer
       ├─ approval-first work → code-brain-planning (lightweight or managed)
       ├─ broad work with unresolved decisions → code-brain-wayfinder → code-brain-planning
       └─ uncertain technical path → tracer-bullet → return to the plan
Approved plan → feature-branch → effective-engineer
Verified work → finalize-implementation → GitHub PR
Delivery → interactive-review (Hunk) → parallel-pr-review
```

Use `domain-modeling` when clarification settles durable terminology or an architectural decision. Approved bounded plans and durable execution slices each run in a fresh worker with only their plan, never the preceding conversation. If the route is unclear, invoke `mystical-tutor`.

## Code Brain workflow

Code Brain keeps durable project memory outside source repositories. Source code remains the implementation and evidence surface; the vault holds strategic intent, plans, domain language, reusable findings, and execution receipts.

Use Code Brain for work that needs a durable plan and approval gate. `code-brain-planning` selects a lightweight single-worker plan or a managed lifecycle from the work's coordination needs; `effective-engineer` handles ordinary work without durable artifacts. Lightweight plans do not need a Kanban card.

### Project spine

Each initialized project has three entry points:

```text
$CODE_BRAIN_ROOT/<repo>/
├── VISION.md                 # human-owned strategy and agent authority
├── AGENTS.md                 # agent-maintained router to active memory
├── KANBAN.md                 # durable managed-work state
├── docs/                     # distilled tutorials, how-to, reference, and explanation
├── plans/<NNN_TOPIC>/        # plan, notes, diagrams, and receipt
├── wayfinding/<NNN_TOPIC>/   # decision maps and tickets
├── todo/                     # durable context for unplanned work
├── domain/                   # glossary, context maps, and ADRs
├── notes/                    # reusable project knowledge
├── resources/                # references and checklists
└── review/                   # review feedback and reusable lessons
```

`docs/` uses [Diátaxis](https://diataxis.fr/) as a compass for tutorials, how-to guides, reference, and explanation; projects create only the categories they need.

Run `code-brain` from the target source repository or one of its worktrees. It resolves `<repo>` from Git so every worktree shares one project folder. A bare invocation audits an existing project and offers a concrete reconciliation without changing the vault first. The first durable workflow bootstraps the spine when `VISION.md` is missing: it reads existing repository and vault context, interviews the user one question at a time, and writes `VISION.md` only after explicit confirmation. Projects are reconciled individually, never bulk-migrated.

`VISION.md` defines purpose, principles, non-goals, and what agents may do without asking. `AGENTS.md` links the board, active plans, and canonical notes; it does not hold task state. `KANBAN.md` is a plain-Markdown board rendered by the [Obsidian Kanban plugin](https://github.com/obsidian-community/obsidian-kanban). Install and enable that plugin to use the board UI.

### Durable planning lifecycle

All `code-brain-planning` plans live under `plans/<NNN_TOPIC>/plan.md` and use `date` and `status` frontmatter with the shared `draft`, `approved`, `implemented`, `abandoned`, and `superseded` lifecycle. Every non-closed plan is linked from `AGENTS.md`.

Lightweight plans record their exploration and delivery outcome in `plan.md`; they have no card or receipt. Managed plans additionally map that lifecycle onto the board:

```text
Inbox → In Progress → Review → Ready → In Progress → Review → Done
                      approval      implementation

Blocked or partial implementation → receipt → Blocked
```

For managed plans:

1. The orchestrator gathers source context and immediately records each useful finding with repository revisions or external URLs before continuing exploration.
2. It writes a numbered `plan.md` with `status: draft`, links it from `AGENTS.md`, and moves its card through drafting and review.
3. Explicit user approval changes the plan to `approved` and moves the card to Ready. Approval does not automatically start implementation.
4. Fresh workers implement their assigned slices. Read-only reviewers check correctness, validation, and simplicity.
5. Accepted work invokes `finalize-implementation` to commit, push, and prepare the pull request.
6. The orchestrator appends an implementation attempt to `receipt.md`, including source evidence for every changed repository. Accepted work becomes `implemented` and moves to Done; blocked, partial, reverted, or unfinalized work remains `approved` and moves to Blocked.

Receipts record the actual commit SHA or a deterministic hash of the complete uncommitted Git change set. Plans preserve design intent, Kanban lanes preserve managed-work state, and receipts preserve what actually happened.

### Supporting workflows

- `domain-modeling` promotes stable terms and hard-to-reverse decisions into the glossary or terse ADRs.
- `code-brain-diagramming` keeps Mermaid diagrams and canvases beside the plan they explain.
- `code-brain-wayfinder` turns uncertain, multi-session work into decision tickets tracked on the Code Brain Kanban board before it becomes a plan.
- `tracer-bullet` proves a risky technical path in an isolated worktree and stores only its durable findings.
- `dreaming` deduplicates session transcripts into reviewable memories before promoting high-confidence knowledge.
- `code-brain-writeback` writes material findings through to activity artifacts as they emerge.
- `gh-pr-review-plan` and `parallel-pr-review` persist feedback and evidence-backed lessons under `review/`.
- `code-brain-distill` promotes reusable findings from activity artifacts into canonical, discoverable documentation under `docs/`.

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
bunx skills add LordPrkr/leonard-lessons --skill agents-md --global
```

Install for a specific agent:

```bash
bunx skills add LordPrkr/leonard-lessons --skill agents-md --agent claude-code --global
```

## Skills

Install the full repository to satisfy dependencies between Leonard Lessons skills. External skills and tools remain separate requirements. For selective installation, use this table; the per-skill commands below are copyable installation bundles.

| Skill or workflow                                                                                                                                     | Required skills and tools                                                                                                                   |
| ----------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `/code-brain`                                                                                                                                         | Pi and Obsidian                                                                                                                             |
| `/code-brain-distill`, `/code-brain-writeback`, `/code-brain-wayfinder`, `/code-brain-diagramming`, `/domain-modeling`, `/dreaming`, `/tracer-bullet` | `/code-brain`                                                                                                                               |
| `/effective-engineer`                                                                                                                                 | External `/tdd` skill                                                                                                                       |
| `/finalize-implementation`                                                                                                                            | `/feature-branch`, `/conventional-commit-message`, `/spellbinding-sentences`, and `gh`                                                   |
| `/code-brain-planning`                                                                                                                                | Core dependencies, plus conditional `/domain-modeling`, `/code-brain-diagramming`, and `/tracer-bullet`                               |
| `/technical-design-proposal`                                                                                                                          | `/spellbinding-sentences`                                                                                                               |
| `/gh-pr-review-plan`, `/parallel-pr-review`                                                                                                           | `gh`, `/code-brain`, and `/code-brain-writeback`                                                                                            |
| `/gh-pr-job-triage`                                                                                                                                   | `gh` and Pi subagents                                                                                                                       |
| `/interactive-review`                                                                                                                                 | cmux and external `/hunk-review`                                                                                                            |
| `/sessions-search`                                                                                                                                   | Local Pi session transcripts                                                                                                                 |

`/code-brain-wayfinder` may route to `/tracer-bullet` or `/code-brain-planning`; install those branches when needed. Install `/domain-modeling` with planning or dreaming when they must capture glossary terms or ADRs. Install the skills that `/mystical-tutor` should route to.

- `mystical-tutor` — recommend the next Leonard Lessons skill and show where
  it leads without starting the work.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill mystical-tutor --global
  ```

- `sessions-search` — locate a topic, decision, implementation detail, or command outcome in local Pi session transcripts.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill sessions-search --global
  ```

- `code-brain` — canonical project spine, Git-native repository resolution,
  Kanban ownership, and durable evidence conventions.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill code-brain --global
  ```

- `code-brain-writeback` — write material findings through to a Code Brain
  activity artifact before continuing exploration or assessment.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill code-brain --global
  bunx skills add LordPrkr/leonard-lessons --skill code-brain-writeback --global
  ```

- `code-brain-distill` — classify reusable plan, review, and dream findings with
  the Diátaxis compass and promote them into canonical Code Brain documentation.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill code-brain --global
  bunx skills add LordPrkr/leonard-lessons --skill code-brain-distill --global
  ```

- `effective-engineer` — tight inspect, red-green implementation, verification,
  and final-review loop for non-trivial code changes.

  ```bash
  bunx skills@latest add mattpocock/skills/skills/engineering/tdd --global
  bunx skills add LordPrkr/leonard-lessons --skill effective-engineer --global
  ```

- `feature-branch` — select or create an appropriately named feature branch
  before implementation or finalization.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill feature-branch --global
  ```

- `code-brain-wayfinder` — chart uncertain, multi-session work as decision
  tickets on the Code Brain Kanban board, then hand the resolved route to
  `code-brain-planning`.

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
  technical path, then recording findings in Code Brain notes.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill code-brain --global
  bunx skills add LordPrkr/leonard-lessons --skill tracer-bullet --global
  ```

- `finalize-implementation` — confirm the feature branch, commit and push the
  verified change, then create its pull request with a finished description.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill feature-branch --global
  bunx skills@latest add conventional-changelog/conventional-changelog/skills/conventional-commit-message --global
  bunx skills add LordPrkr/leonard-lessons --skill spellbinding-sentences --global
  bunx skills add LordPrkr/leonard-lessons --skill finalize-implementation --global
  ```

- `gh-pr-review-plan` — use `gh` to collect human reviewer PR comments,
  persist each assessment and reusable lesson in Code Brain, and plan replies
  or fixes.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill code-brain --global
  bunx skills add LordPrkr/leonard-lessons --skill code-brain-writeback --global
  bunx skills add LordPrkr/leonard-lessons --skill gh-pr-review-plan --global
  ```

- `gh-pr-job-triage` — classify failed pull-request jobs with parallel,
  evidence-gathering scouts.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill gh-pr-job-triage --global
  ```

- `parallel-pr-review` — review a pull request or branch with five fresh,
  read-only reviewers covering intent, correctness, validation, and design fit,
  while persisting feedback and reusable lessons.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill code-brain --global
  bunx skills add LordPrkr/leonard-lessons --skill code-brain-writeback --global
  bunx skills add LordPrkr/leonard-lessons --skill parallel-pr-review --global
  ```

- `interactive-review` — choose the latest commit or a branch comparison, open
  it in a Hunk pane beside the caller terminal, and hand off to `hunk-review`.

  ```bash
  bunx skills@latest add modem-dev/hunk/skills/hunk-review --global
  bunx skills add LordPrkr/leonard-lessons --skill interactive-review --global
  ```

- `code-brain-planning` — approval-first Code Brain planning that chooses a
  lightweight single-worker plan or a managed lifecycle with board transitions
  and implementation receipts.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill code-brain --global
  bunx skills add LordPrkr/leonard-lessons --skill code-brain-writeback --global
  bunx skills add LordPrkr/leonard-lessons --skill domain-modeling --global
  bunx skills add LordPrkr/leonard-lessons --skill spellbinding-sentences --global
  bunx skills add LordPrkr/leonard-lessons --skill feature-branch --global
  bunx skills add LordPrkr/leonard-lessons --skill effective-engineer --global
  bunx skills add LordPrkr/leonard-lessons --skill finalize-implementation --global
  # Add only when the plan needs the corresponding branch.
  bunx skills add LordPrkr/leonard-lessons --skill code-brain-diagramming --global
  bunx skills add LordPrkr/leonard-lessons --skill tracer-bullet --global
  bunx skills add LordPrkr/leonard-lessons --skill code-brain-planning --global
  ```

- `code-brain-diagramming` — add Mermaid diagrams and Obsidian canvases to an
  existing Code Brain plan.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill code-brain --global
  bunx skills add LordPrkr/leonard-lessons --skill code-brain-diagramming --global
  ```

- `spellbinding-sentences` — write explanatory technical docs for readers with
  strong engineering fundamentals, concrete mechanisms, explicit tradeoffs,
  and plain intent over pedantry.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill spellbinding-sentences --global
  ```

- `technical-design-proposal` — turn a cross-boundary system change into a
  reviewable proposal with explicit contracts, trust boundaries, rollout, and
  controls.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill spellbinding-sentences --global
  bunx skills add LordPrkr/leonard-lessons --skill technical-design-proposal --global
  ```

- `domain-modeling` — Code Brain glossary and ADR capture for domain language
  and durable decisions.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill code-brain --global
  bunx skills add LordPrkr/leonard-lessons --skill domain-modeling --global
  ```

- `dreaming` — synthesize local Pi session transcripts into evidence-backed
  Code Brain provenance, then route high-confidence findings to their durable
  owners.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill code-brain --global
  bunx skills add LordPrkr/leonard-lessons --skill domain-modeling --global
  bunx skills add LordPrkr/leonard-lessons --skill dreaming --global
  ```

## Other Useful Skills

### [modem-dev/hunk](https://github.com/modem-dev/hunk)

- `hunk-review` - walk through a changeset or review code using Hunk.

```bash
bunx skills@latest add modem-dev/hunk/skills/hunk-review
```

### [mattpocock/skills](https://github.com/mattpocock/skills)

- `tdd` - test-driven development. Use when the user wants to build features or fix bugs test-first, mentions "red-green-refactor", or wants integration tests.

```bash
bunx skills@latest add mattpocock/skills/skills/engineering/tdd
```

- `resolving-merge-conflicts` - use when you need to resolve an in-progress git merge/rebase conflict.

```bash
bunx skills@latest add mattpocock/skills/skills/engineering/resolving-merge-conflicts
```

- `grilling` - interview the user relentlessly about a plan or design. Use when the user wants to stress-test a plan before building, or uses any 'grill' trigger phrases.

```bash
bunx skills@latest add mattpocock/skills/skills/productivity/grilling
```

- `grill-with-docs` - a relentless interview to sharpen a plan or design, which also creates docs (ADR's and glossary) as we go.

```bash
bunx skills@latest add mattpocock/skills/skills/engineering/grill-with-docs
```

- [`writing-for-agents`](https://github.com/mattpocock/skills/blob/main/skills/productivity/writing-for-agents/SKILL.md) - reference for writing documents that agents consume, including skills and `AGENTS.md` files.

```bash
bunx skills@latest add mattpocock/skills/skills/productivity/writing-for-agents
```

### [vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills)

- `vercel-react-best-practices` - optimize React and Next.js performance.

```bash
bunx skills@latest add vercel-labs/agent-skills/skills/react-best-practices
```

- `vercel-composition-patterns` - design scalable React component APIs.

```bash
bunx skills@latest add vercel-labs/agent-skills/skills/composition-patterns
```

- `web-design-guidelines` - review UI accessibility, design, and UX.

```bash
bunx skills@latest add vercel-labs/agent-skills/skills/web-design-guidelines
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
