---
name: spellbinding-sentences
description: "Draft or revise explanatory technical writing, including design docs, PR descriptions, code review comments, ADRs, incident writeups, architecture notes, and engineering proposals."
---

# Spellbinding Sentences

Explain what happens, why it happens, and what the reader should do next.

## Steps

### 1. Establish what the reader needs

Write for the audience the user names. Otherwise assume readers with strong engineering fundamentals who may not know the local domain or codebase. Explain the unfamiliar concepts they need to follow the argument.

When revising, preserve the original claims, scope, and uncertainty unless the user requests new substance.

Use the evidence already available, keeping clear which claims have been verified. Inspect relevant sources when adding factual claims or resolving ambiguous or conflicting evidence. Label assumptions and claims that remain unverified.

Done when the draft addresses the chosen audience, each factual claim has evidence or explicit uncertainty, and revisions preserve the requested scope.

### 2. Explain how it works

Start each section with its conclusion, change, or proposal. Explain the behavior that supports that point: who or what acts, what it does, and what follows. Name the code path, service, dependency, or condition behind important claims so the reader can connect the explanation to the system.

When the reader must choose, explain each relevant option's benefits, costs, and the conditions that favor it.

For a bug or proposed fix, apply [Explaining failures and fixes](references/FAILURES.md).

Done when the reader can explain why the system behaves as described and has enough information to make any required choice.

### 3. Remove what adds no meaning

Keep one claim per paragraph. Each sentence should support, qualify, or advance that claim. Remove background the audience already knows.

Untangle a dense sentence by stating its simplest true claim, then restoring the conditions and reasons needed to explain it. Use as many sentences as the explanation needs.

Use active verbs and familiar words. Replace invented labels with the behavior they describe. For claims about scale or speed, give numbers or conditions the reader could observe. Keep technical detail that changes what the reader understands or chooses.

Done when each sentence supports its paragraph's claim and the edits preserve the facts, conditions, and reasons behind the conclusion.

## Example: explain why the choice matters

Too compressed:

> Caches trade consistency for speed.

Explanatory:

> A cache makes reads faster by keeping a second copy of data closer to the caller. Once that copy exists, an update to the primary store and an update to the cache may occur at different times or one may fail. Expiration limits how long stale data can survive, but shorter expiration also sends more traffic to the primary store. The right policy depends on the consequence of staleness: an old profile photo may be acceptable, while an old account balance may not be.
