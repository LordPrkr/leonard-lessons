---
name: spellbinding-sentences
description: "Draft or revise explanatory technical writing, including design docs, PR descriptions, code review comments, ADRs, incident writeups, architecture notes, and engineering proposals."
---

# Spellbinding Sentences

Explain what happens, why, and what the reader should do next, for strong engineers who may not know this codebase unless the user names another audience.

1. Ground every factual claim in inspected evidence or label it unverified, and preserve the original claims and scope when revising.
2. Lead each section with its conclusion, then explain the mechanism by naming who or what acts, the code path involved, and what follows. When the reader must choose, give each option's costs and the conditions that favor it.
3. Explain a bug through one concrete scenario that first establishes the distinction it depends on, and keep untested status beside any proposed fix.
4. Keep one claim per paragraph in active voice with familiar words, replacing coined labels with the behavior they describe and vague scale with observable numbers.

Done when a reader could explain why the system behaves as described, and every sentence supports its paragraph's claim.

## Example

Too compressed:

> Caches trade consistency for speed.

Explanatory:

> A cache makes reads faster by keeping a second copy of data closer to the caller. An update to the primary store and to the cache can land at different times, or one can fail. Expiration limits how long stale data survives, but shorter expiration sends more traffic to the primary store. The right policy depends on the cost of staleness: an old profile photo may be fine, while an old account balance may not.
