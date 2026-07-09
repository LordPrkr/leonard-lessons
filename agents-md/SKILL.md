---
name: agents-md
description: "Progressive AGENTS.md authoring and refactoring. Use when the user wants to create, rewrite, slim down, or reorganize AGENTS.md files; mentions progressive disclosure for agent instructions; or asks what belongs in root AGENTS.md versus linked docs."
---

# AGENTS.md

Create or refactor AGENTS.md so the root file is a small router: global facts stay in root, task-specific guidance moves behind links.

## Steps

### 1. Inventory

Read the existing AGENTS.md or source material. Capture each distinct instruction once.

Done when every instruction is listed, deduplicated, and tied to its source text.

### 2. Resolve contradictions

Find instructions that cannot both be followed. For each contradiction, show the conflicting versions and ask the user which one to keep.

Done when every contradiction has a chosen winner, or the draft is blocked on explicit user questions.

### 3. Keep only root essentials

Put only these in root AGENTS.md:

- one-sentence project description
- package manager, only when it is not npm or the repo makes it non-obvious
- non-standard build, test, lint, or typecheck commands
- instructions truly relevant to every task
- markdown links to disclosed guidance files

Done when every root instruction applies repo-wide. If it applies only to one task type, move it behind a link.

### 4. Disclose the rest

Group remaining instructions by when the agent needs them, not by where they came from. Common groups:

- TypeScript conventions
- testing patterns
- API design
- database and migrations
- UI conventions
- Git workflow
- deployment

Create one markdown file per group under a simple docs folder, usually `docs/agents/`.

Done when no instruction appears in two files and each linked file has one clear reason to open it.

### 5. Flag deletion candidates

Flag instructions for deletion when they are:

- redundant with normal agent behavior
- too vague to check
- obvious, like "write clean code"
- duplicated elsewhere

Done when each deletion candidate has a short reason.

### 6. Output or apply the structure

If the user asked for a plan, output:

- minimal root `AGENTS.md`
- each linked markdown file and its contents
- suggested docs folder structure
- deletion list
- unresolved questions

If the user asked you to edit the repo, create or update the files.

Done when the root AGENTS.md is a router and every disclosed file is linked from it.

## Root shape

```md
# AGENTS.md

<one-sentence project description>

## Commands

- Package manager: <pnpm|yarn|bun>
- Typecheck: `<command>`
- Test: `<command>`
- Build: `<command>`

## Project instructions

- <only instructions relevant to every task>

## More guidance

- [TypeScript conventions](docs/agents/typescript.md)
- [Testing patterns](docs/agents/testing.md)
- [API design](docs/agents/api.md)
```

## Pruning rule

If an instruction does not change agent behavior, delete it. If it applies only to one kind of work, move it behind a link.
