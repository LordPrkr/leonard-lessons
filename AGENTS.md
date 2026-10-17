# AGENTS.md

This repository publishes reusable agent skills, one skill per top-level directory.

## Updating skills

- Apply the `writing-for-agents` skill before changing any `SKILL.md`.
- Keep descriptions trigger-focused and instructions general to any user or machine.
- Give every workflow step a checkable completion criterion.
- Keep each rule in one place; move branch-specific reference behind a relative
  Markdown link.
- Update [README.md](./README.md) when adding, removing, renaming, or changing
  dependencies between skills.
- Conclude every verified skill change with
  `$finalize-implementation`, then run
  `bunx skills add . --global --all` from the finalized worktree's repository root.
  Complete only when finalization has finished and installation succeeds.
