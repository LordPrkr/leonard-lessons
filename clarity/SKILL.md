---
name: clarity
description: "Clarity when explaining a problem, proposing a solution, or describing an implementation. Use for initial explanations and revisions when references or jargon are unclear."
---

# Clarity

Make the explanation readable without the source code open. Apply this workflow to the initial explanation and repeat it when the user asks for clarification; return the revised explanation itself.

## Steps

### 1. Invoke spellbinding-sentences

Invoke [/spellbinding-sentences](../spellbinding-sentences/SKILL.md) and apply its explanatory-writing workflow. Use the steps below to make the concrete references and evidence visible to the reader.

Done when the draft satisfies that workflow and preserves the distinction between observed behavior, inference, and proposed changes.

### 2. Name the referents

Inspect the source or supplied material behind the explanation. Replace ambiguous references such as “the query,” “the plugin,” “the function,” “it,” and “this” with the actual SQL statement's location, plugin name, function identifier, or other concrete referent. Include the file path and containing symbol when available. Subsequent shorthand is useful once its antecedent is unambiguous in the same passage.

For unnamed code, identify it by location and purpose, such as “the SQL statement inside `listActiveUsers` in `src/users.ts`.” Label a descriptive name as descriptive rather than implying it is an identifier in the source. If evidence is unavailable, state what is missing and label any example as illustrative.

Done when every reference affecting the explanation resolves to one named object or explicitly identified example, without requiring the reader to search earlier conversation or open a file.

### 3. Resolve jargon

Replace invented shorthand with the concrete behavior it describes. Define necessary domain-specific or otherwise unclear terms at first use: what the term denotes here, which named objects participate, and what happens. Use observable conditions for vague claims such as “slow” or “stale.”

Done when every term needed to follow the reasoning is either ordinary technical vocabulary for the audience or explicitly defined in this explanation, and no coined label substitutes for a mechanism.

### 4. Show the code being discussed

Include fenced, language-tagged excerpts for each SQL query, function, configuration, or other code construct whose behavior the explanation relies on. Introduce each excerpt with its path and identifier, then explain the relevant lines and their consequence.

Show the smallest excerpt that preserves the mechanism: predicates and joins for SQL, relevant inputs and branches for functions, and callers or definitions when they determine the behavior. Mark omissions outside the relevant logic. Quote inspected code accurately; distinguish illustrative code from repository code. A file link supplements an excerpt rather than replacing it.

Done when the reader can verify each code-dependent claim from the included excerpts, with enough surrounding context to understand the behavior.

### 5. Make solutions concrete

When proposing a code change, show a fenced `diff` with the affected path, actual current lines, and proposed replacement lines. Explain how those edits change the behavior described above. The diff may serve as the code excerpt when it contains the necessary context.

Label the diff **proposed**; explaining a solution does not authorize applying it. If the current source is unavailable, label an illustrative diff and state what must be inspected before it becomes an actionable patch. For a new file, show the proposed additions; for a non-code solution, show the specific artifact or operational action instead.

When describing completed work, use the actual resulting code or actual diff and state its implementation and verification status.

Done when every proposed code change has a concrete diff, every completed-change claim matches the inspected result, and the reader can distinguish proposed, illustrative, implemented, and verified work.

### 6. Section and label the response

Organize the explanation under descriptive Markdown headings that match the work's status. For a problem and recommendation, use `## Problem` and `## Proposed Solution`; for completed work and follow-up, use `## Implementation Summary` and `## Next Steps`. Add sections such as `## Verification` or `## Open Questions` when they carry distinct information. Include only sections with substantive content, and place each excerpt or diff beside the claim it supports.

Done when every section's heading accurately labels its content and distinguishes the problem, proposal, completed work, and remaining actions wherever those are present.

### 7. Re-read without the editor

Read the explanation as someone who cannot see the repository. Resolve remaining ambiguous nouns, undefined terms, and unsupported code claims. Keep only excerpts and definitions that support the explanation; retain all evidence needed to follow its reasoning.

Done when the reader can identify what is being discussed, follow why the problem occurs or the implementation works, and see exactly what a proposed solution changes from this explanation alone.
