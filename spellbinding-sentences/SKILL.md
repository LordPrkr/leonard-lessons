---
name: spellbinding-sentences
description: "Spellbinding sentences for technical writing: design docs, PR descriptions, ADRs, incident writeups, architecture notes, and engineering proposals aimed at senior software engineers."
---

# Spellbinding Sentences

Write for a senior software engineer who already knows the domain model and codebase.

## Steps

### 1. Lead with the point

Start each section with what is true, what changed, or what you propose.

Done when no section opens with background, throat-clearing, or a tour of concepts the reader already knows.

### 2. Name the mechanism

Refer to existing code by name: classes, services, modules, jobs, tables, APIs, and call paths.

Done when every important claim is tied to a named code path, system, metric, or failure mode.

### 3. Name the tradeoff

State what the choice buys, what it costs, and which alternative you rejected. Tie recommendations to conditions, not verdicts: "X is cheaper when..." rather than "X is better."

Done when every non-obvious recommendation names its conditions and rejected alternative.

### 4. Motivate only the surprising part

Explain counterintuitive constraints, subtle failure modes, and interactions that are easy to miss. Skip definitions of standard terms and project concepts.

Done when no paragraph restates context the target reader already has.

### 5. Build one concept at a time

Each sentence should rest on the previous one. Do not stack several unexplained ideas in one sentence.

Done when dense paragraphs can be read linearly without requiring the reader to reorder the argument.

### 6. Prefer intent over pedantry

Use the technically precise version when precision changes the decision. Otherwise use the simpler sentence.

Done when edits make the reader's next action clearer, not merely more formally correct.

### 7. Say when there is no clean answer

If the tradeoff is genuinely situational, say so plainly. Explain which conditions move the decision.

Done when ambiguous decisions are not forced into tidy verdicts.

### 8. Start from the kernel sentence

Write the simplest true sentence first. Add only the condition, mechanism, number, or tradeoff that changes the reader's decision.

Done when each dense sentence can be reduced to a clear core claim without losing the argument.

## Style rules

- Use active voice.
- Prefer short declarative sentences.
- Use precise technical terms, with plain connecting prose.
- Use compressed lines rarely, where they land hard.
- Ground claims in specifics: actual latency, throughput, queue depth, retry behavior, storage cost, incident symptoms, named dependencies, or real call paths.
- Replace vague qualifiers like "large," "slow," or "scalable" with numbers or observable conditions.

## Do not

- Open with throat-clearing: "In today's world...", "To understand X...", "X didn't happen overnight..."
- Use contrast cliches: "not just X, but Y" or "isn't merely X — it's Y."
- End paragraphs on hollow punch lines: "The gap is real" or "That changes everything."
- Narrate the document's reasoning: "This is significant because...", "This reinforces...", or "It is important to note..."
- Use filler vocabulary: leverage, robust, seamless, powerful, crucially, ultimately, notably, landscape, navigate, delve.
- Restate the reader's own context back to them.

## Voice target

Match Martin Kleppmann's technical clarity: direct, conditional, concrete, and honest about tradeoffs.

Good pattern:

> Whether using a cloud service is cheaper depends on your ops skills and workload shape. If load is predictable and the team already runs similar systems, owning the machines can be cheaper. If demand spikes unpredictably or operational ownership is thin, the managed service buys elasticity and fewer failure modes at the cost of vendor coupling and higher steady-state spend.

Bad pattern:

> Cloud services are not just infrastructure, but a powerful way to navigate today's scalability landscape.
