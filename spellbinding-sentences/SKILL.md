---
name: spellbinding-sentences
description: "Draft or revise explanatory technical writing for senior engineers, including design docs, PR descriptions, ADRs, incident writeups, architecture notes, and engineering proposals."
---

# Spellbinding Sentences

Write for the audience the user names. Otherwise assume a technically strong reader who does not know the local codebase and wants to understand it quickly.

Concise writing removes information the reader does not need. It does not compress reasoning into slogans. When a mechanism, dependency, or consequence takes three sentences to explain, use three sentences.

## Steps

### 1. Establish the claim

Identify what the reader should understand, decide, or do. If revising, preserve the source's facts, scope, and uncertainty unless the user asks for new substance.

Done when the main claim is explicit and every changed factual claim comes from the source or the user's request.

### 2. Explain the mechanism

Present the idea in the order a reader needs it:

1. the concrete problem or claim;
2. how the relevant system behaves;
3. the consequence of that behavior;
4. the conditions, tradeoffs, or example that make the consequence useful.

Use only the parts the subject requires. A simple fact may need one sentence; a design choice may need all four.

Done when the reader can follow each important conclusion from cause to effect without supplying missing reasoning.

### 3. Spend words on decision-making information

Keep constraints, failure modes, assumptions, numbers, named dependencies, and real code paths. Remove familiar setup and repeated conclusions. Define a term when its local meaning is unfamiliar or narrower than its usual meaning.

Expand any quip, metaphor, or compressed phrase that carries unstated reasoning. A memorable line may summarize an explanation; it may not replace one.

Done when every remaining sentence either explains the claim or changes how the reader should interpret or act on it.

### 4. Test the explanation

Check that recommendations state when they apply, alternatives receive a fair comparison, and examples expose the mechanism rather than merely decorate the prose.

Done when a technically strong reader can state what happens, why it happens, and under which conditions the conclusion changes.

## Writing patterns

- Use plain verbs and precise technical nouns.
- Put the main claim early, then earn it with mechanism and evidence.
- Prefer concrete causality: “The worker retries after the lease expires, so the handler may run twice.”
- Give numbers or observable conditions when magnitude matters.
- Let sentence length follow the reasoning. Short sentences suit simple claims; connected clauses suit connected ideas.
- Use transitions that name the relationship: because, therefore, however, for example, and in contrast.
- End with the consequence or decision, not a catchphrase.

## Examples

These are original examples modeled on the explanatory methods used by Martin Kleppmann, Martin Fowler, and Robert Nystrom.

### Explain a pattern from baseline to consequence

Compressed:

> CQRS splits reads from writes. Simple idea, big consequences.

Explanatory:

> A conventional CRUD model uses the same representation for reads and writes. CQRS separates them: commands update a write model, while queries read from a model shaped for display or retrieval. This can simplify a domain whose validation rules and query shapes pull the shared model in different directions. It also introduces synchronization and consistency work, so it is usually justified only for the parts of a system where those benefits exceed the added complexity.

The second version defines the baseline, describes the mechanism, and states both the benefit and its limit. This follows Fowler’s progression in [CQRS](https://martinfowler.com/bliki/CQRS.html).

### Follow the hidden mechanism

Compressed:

> Caches trade consistency for speed.

Explanatory:

> A cache makes reads faster by keeping a second copy of data closer to the caller. Once that copy exists, an update to the primary store and an update to the cache may occur at different times or one may fail. Expiration limits how long stale data can survive, but shorter expiration also sends more traffic to the primary store. The right policy depends on the consequence of staleness: an old profile photo may be acceptable, while an old account balance may not be.

The second version turns a slogan into a model the reader can use to reason about failure and choose a policy. This reflects the mechanism-and-tradeoff method used throughout Kleppmann’s *Designing Data-Intensive Applications*.

### Use an example to make an abstraction operational

Compressed:

> A closure is a function with a backpack of variables.

Explanatory:

> A closure pairs a function with the environment in which the function was declared. If the function refers to a local variable and escapes its declaring scope, that environment must remain available after the outer call returns. Two closures created by separate calls therefore retain separate instances of the same local variable. The implementation must preserve those captured bindings rather than treating them like ordinary stack locals.

The metaphor may help memory, but the explanation tells the reader what must persist and why the runtime needs special handling. This follows the concrete-to-implementation progression in Nystrom’s [Crafting Interpreters](https://craftinginterpreters.com/closures.html).

## Voice target

Aim for the shared strengths of these writers:

- **Kleppmann:** explain internal behavior, then compare designs by workload and failure mode.
- **Fowler:** introduce the ordinary model before the pattern that departs from it; state where the pattern is a poor fit.
- **Nystrom:** build intuition with a concrete example, then connect it to the implementation.

Use their explanatory discipline, not their mannerisms.
