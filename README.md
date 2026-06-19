# Leonard Lessons 🪄

Public agent skills from Leonard the Orange 🐦‍🔥

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
- `code-brain-planning` — durable Code Brain planning workflow for broad, risky, cross-cutting, or approval-first changes.

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

- `domain-modeling` - Build and sharpen a project's domain model. Use when the user wants to pin down domain terminology or a ubiquitous language, record an architectural decision, or when another skill needs to maintain the domain model.

```
npx skills@latest add mattpocock/skills/skills/engineering/domain-modeling
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
