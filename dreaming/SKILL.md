---
name: dreaming
disable-model-invocation: true
description: "Curate local Pi session transcripts into Code Brain memory."
---

# Dreaming

A dream is a synthesis pass over past sessions. It turns scattered transcript evidence from `~/.pi/agent/sessions/` into durable Code Brain memory.

Use `/code-brain` repo resolution and store artifacts in `~/Documents/Code Brain/<repo>/`. Treat transcripts as evidence, not memory.

Invoke `domain-modeling` when a dream surfaces domain language, bounded contexts, or architectural decisions worth promoting.

## Steps

### 1. Select Sessions

Resolve the current repo with `/code-brain`. Find session JSONL files under `~/.pi/agent/sessions/` whose opening `session.cwd` belongs to the repo or one of its worktrees.

Default to the latest 10 matching sessions unless the user gives a count, date range, repo, or explicit paths. Ignore sessions with no meaningful user/assistant work.

Done when every selected session is listed with path, timestamp, cwd, and a one-line topic.

### 2. Dream

Read the selected transcripts and extract only durable memory:

- Parker preferences
- repeated workflow habits
- repo-specific architecture or domain discoveries
- commands, tests, or verification loops worth reusing
- recurring failure modes
- decisions worth remembering
- useful reusable plans or patterns

Drop one-off debugging chatter, transient logs, failed guesses, secrets, and duplicates already captured in Code Brain.

Every insight must cite at least one session path plus timestamp or message summary.

Done when each candidate insight has evidence, an applicability boundary, and confidence: `high`, `medium`, or `low`.

### 3. Write the Dream Note

Create `notes/dreams/YYYY-MM-DD Dream.md` in the repo's Code Brain folder.

Template:

```md
# Dream — YYYY-MM-DD

## Sessions Dreamed

- `<path>` — timestamp — topic

## Durable Memories

### Preference / Pattern / Architecture / Workflow

- Insight:
- Evidence:
- Applies when:
- Confidence: high | medium | low

## Contradictions or Stale Memories

- Existing memory:
- New evidence:
- Suggested replacement:

## Follow-up Work

- [ ] Optional cleanup or documentation task
```

Done when the dream note is written and every durable memory links back to transcript evidence.

### 4. Promote Canonical Memories

Update canonical Code Brain files only for high-confidence insights that clearly belong there. Use `domain-modeling` for domain terms, bounded contexts, and ADR-worthy decisions:

- `domain/CONTEXT.md` for domain terms
- `resources/Agent Memory.md` for Parker or repo workflow preferences
- `notes/<topic>.md` for reusable project context

Do not promote low-confidence or one-off insights. The dream note is the reviewable staging area.

Done when every promoted insight has one source of truth, and unpromoted insights remain only in the dream note.

### 5. Report

Summarize the dream note path, promoted files, skipped stale or duplicate items, and any follow-up tasks.

Done when the user can review the dream without rereading the transcripts.
