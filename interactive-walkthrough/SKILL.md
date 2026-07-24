---
name: interactive-walkthrough
description: "Explain a commit or branch diff interactively in Hunk."
disable-model-invocation: true
---

# Interactive Walkthrough

Walk through every changed block in Hunk. Explain the code rather than auditing
it for defects. Run from the repository being explained.

## 1. Choose the target

Ask:
`Walk through the latest commit (HEAD), or the current branch against another branch?`

- For the latest commit, resolve `HEAD` to its commit SHA.
- For a branch walkthrough, ask for the base branch, then resolve the base branch
  and `HEAD` to commit SHAs. Compare `<base-sha>...<head-sha>`.

Use Git to verify the repository and refs. Stop if the branch diff is empty.

**Complete when:** the repository root and immutable commit or branch-diff SHAs
are known.

## 2. Open Hunk beside the caller terminal

Resolve `hunk` to an absolute path with `command -v hunk` in the caller's
shell before opening the terminal. Use `cmux_open_terminal` with placement
`"right"` to open a pane in the current cmux tab. Shell-quote the working
directory and resolved path, then run exactly one target:

```bash
cd -- '<repository-root>' && '<absolute-hunk-path>' show <commit-sha>
cd -- '<repository-root>' && '<absolute-hunk-path>' diff <base-sha>...<head-sha>
```

Title the pane `Hunk Walkthrough`. Do not run the Hunk TUI in the agent's
terminal or open a different cmux workspace.

**Complete when:** `hunk session get --repo <repository-root>` finds the live
session showing the selected immutable target.

## 3. Explain every changed block

Invoke `/spellbinding-sentences`, then `/hunk-review` for the live session. Use
Hunk's review structure to account for every changed block, grouping adjacent
blocks only when they implement the same mechanism.

For each block:

1. Navigate Hunk to it.
2. Lead with what the block changes.
3. Ground the explanation in the exact symbols and code path.
4. Explain why it exists and how it contributes to the larger change.
5. Name a tradeoff or risk only when it changes how the block should be
   understood.

Prefer narration and focused explanatory comments over defect hunting. Mention
a correctness concern if one appears, but do not turn the walkthrough into a
code review.

**Complete when:** every changed block is explained or explicitly grouped under
one shared explanation, and the walkthrough ends with the change's end-to-end
flow.
