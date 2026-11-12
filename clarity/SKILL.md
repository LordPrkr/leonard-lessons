---
name: clarity
description: "Clarity when explaining a problem, proposing a solution, or describing an implementation. Use for initial explanations and revisions when references or jargon are unclear."
---

# Clarity

Apply `$spellbinding-sentences`, then make the explanation readable without the source open.

1. Replace vague referents ("the query", "it") with the named file, symbol, or statement, and define any domain term or coined label at first use.
2. Show a short, language-tagged excerpt of each piece of code the explanation relies on, introduced with its path and identifier.
3. Show each proposed change as a `diff` labeled **proposed**, and describe completed work with the actual diff and its verification status.
4. Use headings that match the status of the work, such as `## Problem` and `## Proposed Solution`, or `## Implementation Summary` and `## Next Steps`.

Done when a reader without the repository can tell what is discussed, why it behaves that way, and exactly what changes.
