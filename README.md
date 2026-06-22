# Leonard Lessons 🪄

Public agent skills from Leonard the Orange 🐦‍🔥

These skills use a "Code Brain" Obsidian vault at `~/Documents/Code Brain` for planning, domain notes, and ADRs. Project folders are resolved by canonical repo name; see [`CODE_BRAIN_LOCATION.md`](CODE_BRAIN_LOCATION.md) for worktree-safe rules. They treat the code repository as evidence and implementation, not the documentation store.

## Install

List available skills:

```bash
npx skills add LordPrkr/leonard-lessons --list
```

Install all skills interactively:

```bash
npx skills add LordPrkr/leonard-lessons
```

Install one skill globally:

```bash
npx skills add LordPrkr/leonard-lessons --skill effective-engineer --global
```

Install for a specific agent:

```bash
npx skills add LordPrkr/leonard-lessons --skill effective-engineer --agent claude-code --global
```

## Skills

- `effective-engineer` — tight inspect, test, implement, verify, and summarize loop for non-trivial code changes.

  ```bash
  npx skills add LordPrkr/leonard-lessons --skill effective-engineer --global
  ```

- `code-brain-planning` — durable Code Brain planning workflow for broad, risky, cross-cutting, or approval-first changes.

  ```bash
  npx skills add LordPrkr/leonard-lessons --skill code-brain-planning --global
  ```

- `domain-modeling` — Code Brain glossary and ADR capture for domain language and durable decisions.

  ```bash
  npx skills add LordPrkr/leonard-lessons --skill domain-modeling --global
  ```

## Other Useful Skills

### [mattpocock/skills](mattpocock/skills)

- `tdd` - test-driven development. Use when the user wants to build features or fix bugs test-first, mentions "red-green-refactor", or wants integration tests.

```
npx skills@latest add mattpocock/skills/skills/engineering/tdd
```

- `grilling` - interview the user relentlessly about a plan or design. Use when the user wants to stress-test a plan before building, or uses any 'grill' trigger phrases.

```
npx skills@latest add mattpocock/skills/skills/productivity/grilling
```

- `grill-with-docs` - a relentless interview to sharpen a plan or design, which also creates docs (ADR's and glossary) as we go.

```
npx skills@latest add mattpocock/skills/skills/engineering/grill-with-docs
```

- `writing-great-skills` - reference for writing and editing skills well — the vocabulary and principles that make a skill predictable.

```bash
npx skills@latest add mattpocock/skills/skills/productivity/writing-great-skills
```

### [cmux](https://cmux.com/docs/skills)

```bash
npx skills add manaflow-ai/cmux -g -y
```
