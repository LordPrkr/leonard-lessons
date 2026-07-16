# Leonard Lessons 🪄

Public agent skills from Leonard the Orange 🐦‍🔥

These skills provide a bespoke, local-first Pi + Obsidian workflow. Code Brain stores durable project memory separately from source repositories. Set `CODE_BRAIN_ROOT` to a non-empty vault path or use the default `~/Documents/Code Brain`.

Durable projects have a human-owned `VISION.md`, an agent-maintained `AGENTS.md` router, and a plain-Markdown `KANBAN.md` work board rendered by the [Obsidian Kanban plugin](https://github.com/obsidian-community/obsidian-kanban). Install and enable that community plugin in Obsidian. Durable planning invokes Code Brain bootstrap with the user's confirmation when `VISION.md` is missing; existing vault content is not bulk-migrated. Plans own design lifecycle, Kanban lanes own task state, and appendable receipts own execution results.

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

Dependencies: these workflows require Pi and Obsidian. Install `code-brain` before `domain-modeling`, `code-brain-diagramming`, `code-brain-planning`, `dreaming`, or `tracer-bullet`. Install `domain-modeling` with `code-brain-planning` or `dreaming` when plans or dreams need glossary or ADR capture.

- `code-brain` — canonical project spine, Git-native repository resolution,
  Kanban ownership, and durable evidence conventions.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill code-brain --global
  ```

- `effective-engineer` — tight inspect, test, implement, verify, and
  summarize loop for non-trivial code changes.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill effective-engineer --global
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
