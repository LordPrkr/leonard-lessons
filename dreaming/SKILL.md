---
name: dreaming
disable-model-invocation: true
description: "Idempotently curate local Pi session transcripts into durable Code Brain memory."
---

# Dreaming

A dream synthesizes past Pi sessions from `~/.pi/agent/sessions/` into durable Code Brain memory. Use `/code-brain` for repository identity, vault location, and evidence. Transcripts are local evidence, not canonical memory.

Invoke `domain-modeling` when a dream surfaces domain language, bounded contexts, or ADR-worthy decisions.

## Steps

### 1. Select sessions

Find session JSONL files whose opening `session.cwd` belongs to the resolved repository or one of its worktrees. Use the opening `session.id` as the stable key; only when it is absent use the resolved JSONL path. Sort sessions by opening timestamp, then stable key.

Default to the latest 10 matching meaningful sessions unless the user gives a count, range, repository, or explicit paths. When today's dream note already exists, combine its recorded sessions with newly selected sessions so synthesis covers the complete same-day set rather than overwriting it.

Done when each selected session has stable key, path, opening timestamp, cwd, and one-line topic.

### 2. Synthesize the complete set

Recompute candidate memories across the complete session set whenever sessions are added. Extract only durable preferences, repeated workflows, repository architecture or domain discoveries, reusable commands and patterns, recurring failures, and decisions.

Drop one-off chatter, transient logs, guesses, secrets, and memories already canonical. Deduplicate identical evidence entries by stable key. Deduplicate insights by normalized heading plus normalized claim text. Each retained insight needs evidence, applicability boundary, and confidence: `high` for an explicit user decision, authoritative source, or repeated corroboration; `medium` for one clear session observation; `low` for inference or a tentative pattern.

Done when every retained insight has evidence, an applicability boundary, and evidence-based confidence, and rerunning with the same sessions produces no duplicate session, evidence, or insight entry.

### 3. Merge the dream note

Read [`references/TEMPLATE.md`](references/TEMPLATE.md). Create or merge `notes/dreams/YYYY-MM-DD Dream.md`; never replace a same-day note wholesale. Regenerate only the marked managed entries keyed by stable session or insight ID; preserve all text outside those entries as human-owned.

Apply `/code-brain`'s evidence convention when the note makes source-backed or external claims. Session evidence uses stable session IDs as local-only leads, with durable claims summarized in the note.

Done when the note covers the complete same-day set and every insight points to deduplicated evidence.

### 4. Reconcile canonical memory

Promote only high-confidence insights that clearly belong in canonical files:

- the context selected by `domain-modeling` for domain terms
- `resources/Agent Memory.md` for user or repository workflow preferences
- `notes/<topic>.md` for reusable project context

Before replacing or removing contradicted high-confidence canonical memory, show the user the exact existing text, proposed replacement or removal, and supporting evidence. Change it only after confirmation. Update glossary definitions in place and use `domain-modeling` for ADR supersession. Low-confidence and one-off insights remain only in the dream note.

Done when each promoted insight has one source of truth and no contradicted canonical statement was silently retained or changed.

### 5. Report

Report the dream note path, newly merged session keys, promoted files, deduplicated or stale items skipped, contradictions awaiting confirmation, and follow-up work.

Done when the user can review merged sessions, promotions, skips, and pending contradictions without rereading transcripts.
