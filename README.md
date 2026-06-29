# Leonard Lessons 🪄

Public agent skills from Leonard the Orange 🐦‍🔥

These skills use a "Code Brain" Obsidian vault at `~/Documents/Code Brain` for planning, domain notes, ADRs, resources, and review notes. The `/code-brain` skill owns folder structure and worktree-safe repo resolution. They treat the code repository as evidence and implementation, not the documentation store.

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

- `code-brain` — shared Code Brain structure and worktree-safe project folder conventions.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill code-brain --global
  ```

- `effective-engineer` — tight inspect, test, implement, verify, and summarize loop for non-trivial code changes.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill effective-engineer --global
  ```

- `gh-pr-review-plan` — use `gh` to collect human reviewer PR comments,
  assess them, and plan replies or fixes.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill gh-pr-review-plan --global
  ```

- `code-brain-planning` — durable Code Brain planning workflow for broad, risky, cross-cutting, or approval-first changes. Depends on `/code-brain`.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill code-brain --global
  bunx skills add LordPrkr/leonard-lessons --skill code-brain-planning --global
  ```

- `domain-modeling` — Code Brain glossary and ADR capture for domain language and durable decisions. Depends on `/code-brain`.

  ```bash
  bunx skills add LordPrkr/leonard-lessons --skill code-brain --global
  bunx skills add LordPrkr/leonard-lessons --skill domain-modeling --global
  ```

## Other Useful Skills

### [mattpocock/skills](mattpocock/skills)

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
