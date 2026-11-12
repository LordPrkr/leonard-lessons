---
name: agents-md
description: "Progressive AGENTS.md authoring and refactoring. Use when the user wants to create, rewrite, slim down, or reorganize AGENTS.md files; mentions progressive disclosure for agent instructions; or asks what belongs in root AGENTS.md versus linked docs."
---

# AGENTS.md

Make root `AGENTS.md` a small router: facts every task needs stay in root, and task-specific guidance moves behind links.

## 1. Inventory

List each distinct instruction once, and ask the user to resolve any pair that cannot both be followed.

Done when every instruction is deduplicated and every contradiction has a chosen winner.

## 2. Sort

Keep in root only the project description, non-obvious package manager and commands, rules for every task, and links; move the rest into files such as `docs/agents/<topic>.md` linked with a one-line reason to open each. Flag for deletion anything the agent already does by default, too vague to check, or duplicated.

Done when every instruction is in root, behind a link, or on the deletion list with a reason.

## 3. Output or apply

Output the proposed files and deletion list when asked for a plan; otherwise edit in place, preserving unrelated content.

Done when every relative link resolves and root reads like the shape below.

```md
# AGENTS.md

<one-sentence project description>

## Commands
- Test: `<command>`

## Project instructions
- <rules for every task>

## More guidance
- [Testing patterns](docs/agents/testing.md)
```
