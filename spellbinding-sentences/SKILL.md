---
name: spellbinding-sentences
description: "Use when drafting or revising technical writing for senior engineers: design docs, PR descriptions, ADRs, incident writeups, architecture notes, or engineering proposals."
---

# Spellbinding Sentences

Write for a senior software engineer who already knows the domain model and codebase.

## Steps

### 1. Preserve the facts

If revising, keep the original claims, scope, and uncertainty unless the user asks for new substance.

Done when every changed claim is either present in the source or explicitly requested.

### 2. Lead with the point

Start each section with what is true, what changed, or what you propose.

Done when no section opens with background, throat-clearing, or a tour of concepts the reader already knows.

### 3. Ground claims in mechanisms

Name the code path, service, metric, failure mode, dependency, or operational condition behind important claims.

Done when every important claim has a concrete anchor.

### 4. State the tradeoff

Say what the choice buys, what it costs, when it wins, and what alternative it rejects. Tie recommendations to conditions, not verdicts: "X is cheaper when..." rather than "X is better."

Done when every non-obvious recommendation is conditional and names its rejected alternative.

### 5. Cut inherited context

Explain only the surprising constraint, subtle failure mode, or decision-moving detail. Skip definitions of standard terms and project concepts.

Done when no paragraph restates context the target reader already has.

### 6. Make paragraphs linear

Each paragraph should make one claim. Each sentence should support, qualify, or advance that claim.

Done when no sentence introduces an unexplained second argument.

### 7. Prefer intent over pedantry

Use the technically precise version when precision changes the decision. Otherwise use the simpler sentence.

Done when edits make the reader's next action clearer, not merely more formally correct.

### 8. Tighten from the kernel sentence

Reduce each dense sentence to its simplest true claim, then add back only the condition, mechanism, number, or tradeoff that changes the reader's decision.

Done when every sentence is precise without becoming ceremonial.

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
