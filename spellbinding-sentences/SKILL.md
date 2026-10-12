---
name: spellbinding-sentences
description: "Draft or revise explanatory technical writing, including design docs, PR descriptions, code review comments, ADRs, incident writeups, architecture notes, and engineering proposals."
---

# Spellbinding Sentences

Write for the audience the user names. Otherwise assume the reader is technical, has strong engineering fundamentals, and may not know the local domain or codebase.

Concise writing removes information the reader does not need. It does not compress reasoning into slogans. When a mechanism, dependency, or consequence takes three sentences to explain, use three sentences.

## Steps

### 1. Preserve the facts

If revising, keep the original claims, scope, and uncertainty unless the user asks for new substance.

Verify factual claims against the relevant source evidence, such as code, schemas, API contracts, or supplied material. Mark assumptions and claims that remain unverified.

Done when every factual claim is supported by source evidence or marked unverified, and revisions preserve the original scope and uncertainty unless the user requested a change.

### 2. Lead with the point

Start each section with what is true, what changed, or what you propose.

Done when no section opens with generic background or a tour of concepts the reader already knows.

### 3. Ground claims in mechanisms

Name the code path, service, metric, failure mode, dependency, or operational condition behind important claims. Explain the relevant chain of cause and effect: what the system does, why it does it, and what follows.

Explain unfamiliar concepts the reader needs to understand the claim.

When explaining a bug or proposing a fix, apply [Explaining failures and fixes](references/FAILURES.md).

Done when every important claim has a concrete anchor, necessary unfamiliar concepts are explained, and the reader can follow each conclusion without supplying missing reasoning. For a failure example, check: **Can the reader explain why the example fails without knowing the codebase?**

### 4. Explain trade-offs when the reader must choose

When the reader needs to choose between options, explain what each relevant option buys, what it costs, and the conditions that favor it. A bug explanation can proceed directly from the failure to the fix when no choice needs explaining.

Done when each choice the reader needs to make has enough trade-off information to decide, or the writing requires no choice between options.

### 5. Cut inherited context

Explain only the surprising constraint, subtle failure mode, or detail that changes the decision and that the target reader does not already know. Skip definitions of standard terms.

Done when no paragraph restates context the target reader already has.

### 6. Make paragraphs linear

Each paragraph should make one claim. Each sentence should support, qualify, or advance that claim.

Done when no sentence introduces an unexplained second argument.

### 7. Prefer intent over pedantry

Use the technically precise version when precision changes the decision. Otherwise use the simpler sentence.

Done when edits make the reader's next action clearer, not merely more formally correct.

### 8. Tighten from the kernel sentence

Reduce each dense sentence to its simplest true claim, then add back the condition, mechanism, number, or trade-off needed to explain it. Use plain words and explicit clauses in place of invented jargon or compound modifiers that hide a relationship the reader needs. A memorable phrase may summarize an explanation; it may not replace one.

Done when every sentence is precise, every necessary relationship is explicit, and no sentence becomes a slogan through editing.

## Style rules

- Use active voice.
- Prefer direct declarative sentences. Let sentence length follow the reasoning.
- Replace vague qualifiers like "large," "slow," or "scalable" with numbers or observable conditions.
- Use transitions that name the relationship: because, therefore, however, for example, and in contrast.

## Do not

- Open with generic background: "In today's world...", "To understand X...", "X didn't happen overnight..."
- Use contrast cliches: "not just X, but Y" or "isn't merely X — it's Y."
- End paragraphs on hollow punch lines: "The gap is real" or "That changes everything."
- Narrate the document's reasoning: "This is significant because...", "This reinforces...", or "It is important to note..."
- Use filler vocabulary: leverage, robust, seamless, powerful, crucially, ultimately, notably, landscape, navigate, delve.

## Examples

### Explain a pattern from its baseline

Too compressed:

> CQRS splits reads from writes. Simple idea, big consequences.

Explanatory:

> A conventional CRUD model uses the same representation for reads and writes. CQRS separates them: commands update a write model, while queries read from a model shaped for display or retrieval. This can simplify a domain whose validation rules and query shapes pull the shared model in different directions. It also introduces synchronization and consistency work, so it is usually justified only for the parts of a system where those benefits exceed the added complexity.

The second version defines the ordinary model, describes what CQRS changes, and states both the benefit and its limit.

### Follow the mechanism to its consequence

Too compressed:

> Caches trade consistency for speed.

Explanatory:

> A cache makes reads faster by keeping a second copy of data closer to the caller. Once that copy exists, an update to the primary store and an update to the cache may occur at different times or one may fail. Expiration limits how long stale data can survive, but shorter expiration also sends more traffic to the primary store. The right policy depends on the consequence of staleness: an old profile photo may be acceptable, while an old account balance may not be.

The second version gives the reader a model for reasoning about failure and choosing a policy.

### Connect an abstraction to its implementation

Too compressed:

> A closure is a function with a backpack of variables.

Explanatory:

> A closure pairs a function with the environment in which the function was declared. If the function refers to a local variable and escapes its declaring scope, that environment must remain available after the outer call returns. Two closures created by separate calls therefore retain separate instances of the same local variable. The implementation must preserve those captured bindings rather than treating them like ordinary stack locals.

The metaphor may help memory, but the explanation tells the reader what must persist and why the runtime needs special handling.
