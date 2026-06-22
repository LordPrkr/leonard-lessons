---
name: domain-modeling
description: "Code Brain domain modeling. Use when planning reveals domain language, ubiquitous language, bounded contexts, or architectural decisions that should be captured in the Code Brain instead of the repo."
---

# Domain Modeling

Build the domain model in the Code Brain project folder's `domain/` directory, not in the source repo. Resolve that folder using `../CODE_BRAIN_LOCATION.md`; this matters in git worktrees. Treat code as evidence, not the storage location.

## Files

Single context:

```txt
domain/
├── CONTEXT.md
└── docs/adr/
```

Multiple contexts:

```txt
domain/
├── CONTEXT-MAP.md
├── docs/adr/                 # system-wide decisions
└── contexts/
    ├── ordering/CONTEXT.md
    └── billing/CONTEXT.md
```

Create files lazily: first resolved term creates `CONTEXT.md`; first qualifying decision creates `docs/adr/0001-*.md`.

## ADRs

ADRs live in Code Brain, not the repo. Use `domain/docs/adr/` for system-wide decisions and `domain/contexts/<context>/docs/adr/` for context-specific decisions. Number by scanning the target `docs/adr/` directory and incrementing the highest `NNNN-*` file.

Template:

```md
# {Short title}

{1-3 sentences: context, decision, and why.}
```

Optional sections (`Status`, `Considered Options`, `Consequences`) are allowed only when they add useful memory.

## During Planning

### Challenge language

When a term conflicts with the Code Brain glossary, call it out immediately.

Done when the user chooses the canonical meaning or name.

### Sharpen terms

When language is fuzzy or overloaded, propose one canonical term and avoided names.

Done when the term can be added as `**Term**: definition` plus optional `_Avoid_:` names.

### Cross-check code

When the user states how the domain works, check the source code for agreement.

Done when contradictions are surfaced as questions, not silently encoded.

### Update Code Brain

Write resolved terms to the relevant Code Brain `domain/**/CONTEXT.md` immediately. Keep implementation details out.

Done when every resolved domain term from the session is captured in the Code Brain.

### Offer ADRs sparingly

Create a Code Brain ADR only when all three are true:

1. Hard to reverse.
2. Surprising without context.
3. A real trade-off with reasonable alternatives.

Good ADRs capture architectural shape, integration boundaries, lock-in technology choices, ownership boundaries, non-obvious constraints, and rejected alternatives worth remembering. Skip easy, obvious, or no-alternative decisions.

Done when qualifying decisions are recorded under `domain/docs/adr/` or the relevant context's `docs/adr/` and linked from the plan.
