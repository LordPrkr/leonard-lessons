---
name: domain-modeling
description: "Direct Code Brain glossary and terse ADR work, plus domain capture during durable planning and dreaming. Use when language, bounded contexts, or architectural decisions need a durable source of truth."
---

# Domain Modeling

Build the domain model in `/code-brain`'s project folder under `domain/`, not in the source repository. Treat code as evidence and follow `/code-brain`'s evidence convention for source-backed or external claims.

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
├── docs/adr/
└── contexts/
    ├── ordering/CONTEXT.md
    └── billing/CONTEXT.md
```

Create files lazily. Before writing the first term, use [`references/CONTEXT-FORMAT.md`](./references/CONTEXT-FORMAT.md) to select its context. A system-wide or single-context term creates `domain/CONTEXT.md`; a context-specific term creates `domain/contexts/<context>/CONTEXT.md`. Create `domain/CONTEXT-MAP.md` when the project has multiple bounded contexts. The first qualifying decision creates the appropriate `docs/adr/0001-*.md`. Update an existing glossary term in place rather than adding a competing definition.

## ADRs

Use `domain/docs/adr/` for system-wide decisions and `domain/contexts/<context>/docs/adr/` for context-specific decisions. Number by scanning the target directory and incrementing its highest `NNNN-*` file.

Keep ADRs terse:

```md
# {Short title}

{1-3 sentences: context, decision, and why.}
```

Optional `Status`, `Considered Options`, `Consequences`, and evidence sections are allowed only when they add useful memory. Create an ADR only when the decision is all three:

1. Hard to reverse.
2. Surprising without context.
3. A real trade-off with reasonable alternatives.

When a decision changes, create a replacement ADR. Mark the old ADR `Superseded by <relative Markdown link to new ADR>` and add `Supersedes <relative Markdown link to old ADR>` to the replacement. Do not rewrite the historical decision as though it never happened.

## Workflow

### 1. Resolve language

Challenge terms that conflict with the glossary and let the user choose the canonical meaning or name. For fuzzy or overloaded language, propose one `**Term**: definition` and optional `_Avoid_:` names.

Done when each candidate term has one agreed meaning or one explicit blocking question.

### 2. Test boundaries

Stress-test fuzzy relationships with concrete edge-case scenarios that force their boundaries to become explicit.

Done when each resolved relationship has an applicability boundary.

### 3. Verify claims

Cross-check claims against source and present contradictions as questions for resolution.

Done when each material claim has durable evidence or an explicit unresolved contradiction.

### 4. Persist the model

Select the context using `CONTEXT-FORMAT.md`, then update resolved terms immediately in the relevant `domain/**/CONTEXT.md`.

Done when each resolved term has one definition in exactly one context glossary.

### 5. Capture decisions

Offer ADRs only at the threshold above and link created ADRs from the active plan or dream.

Done when each qualifying decision is recorded, and each changed decision has reciprocal supersession links.
