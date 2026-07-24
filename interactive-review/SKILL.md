---
name: interactive-review
description: "Open Hunk beside the caller terminal and hand off an interactive review."
disable-model-invocation: true
---

# Interactive Review

Launch the review target in Hunk, then let `/hunk-review` control the live
session. Run from the repository being reviewed.

## 1. Choose the target

Ask: `Review the latest commit (HEAD), or the current branch against another branch?`

- For the latest commit, resolve `HEAD` to its commit SHA.
- For a branch review, ask for the base branch, then resolve the base branch and
  `HEAD` to commit SHAs. Compare `<base-sha>...<head-sha>`.

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

Title the pane `Hunk Review`. Do not run the Hunk TUI in the agent's terminal or
open a different cmux workspace.

**Complete when:** `hunk session get --repo <repository-root>` finds the live
session showing the selected immutable target.

## 3. Walk the review

Invoke `/hunk-review` for the live session. Let it inspect the diff structure,
navigate the user through important hunks, add focused comments when useful,
and summarize the review.

**Complete when:** `/hunk-review` has walked the selected target and summarized
its findings.
