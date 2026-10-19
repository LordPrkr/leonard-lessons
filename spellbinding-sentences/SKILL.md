---
name: spellbinding-sentences
description: "Draft or revise explanatory technical writing, including design docs, PR descriptions, code review comments, ADRs, incident writeups, architecture notes, and engineering proposals."
---

# Spellbinding Sentences

## Steps

### 1. Establish the facts and audience

Write for the named audience; otherwise assume technical readers with strong engineering fundamentals who may not know the local domain or codebase. When revising, preserve the original claims, scope, and uncertainty unless the user requests new substance.

Reuse supplied evidence and established verification status. Inspect relevant sources when adding factual claims, resolving ambiguity, or finding contradictions. Label assumptions and unverified claims.

Done when material claims have supporting evidence or explicit uncertainty, and revisions preserve the requested substance.

### 2. Explain the point and mechanism

Lead each section with the conclusion, change, or proposal. Establish the context and unfamiliar concepts the audience needs, then explain the concrete behavior and its consequences. Anchor important claims in a code path, dependency, metric, or observable condition.

When the reader must choose, explain what each relevant option buys, what it costs, and which conditions favor it. When explaining a bug or proposing a fix, apply [Explaining failures and fixes](references/FAILURES.md).

Done when the reader can follow each conclusion and make any required choice without supplying missing context or causal reasoning.

### 3. Edit for clarity

Keep one claim per paragraph; each sentence should support, qualify, or advance it. Reduce dense sentences to their simplest true claim, then restore the conditions and causal relationships needed to explain it. Let sentence length follow the reasoning.

Use active voice, plain words, explicit clauses, and numbers or observable conditions for claims about scale or speed. Retain technical precision where it changes the reader's understanding or decision. State mechanisms and consequences directly, keeping words that add meaning and context the audience needs.

Done when the explanation preserves its facts and causal chain, each sentence supports its paragraph's claim, and removing more would lose necessary meaning.

## Example: mechanism, consequence, and trade-off

Too compressed:

> Caches trade consistency for speed.

Explanatory:

> A cache makes reads faster by keeping a second copy of data closer to the caller. Once that copy exists, an update to the primary store and an update to the cache may occur at different times or one may fail. Expiration limits how long stale data can survive, but shorter expiration also sends more traffic to the primary store. The right policy depends on the consequence of staleness: an old profile photo may be acceptable, while an old account balance may not be.
