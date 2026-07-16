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

Create files lazily. The first resolved term creates `CONTEXT.md`; the first qualifying decision creates `docs/adr/0001-*.md`. Update an existing glossary term in place rather than adding a competing definition. Read [`references/CONTEXT-FORMAT.md`](./references/CONTEXT-FORMAT.md) before creating or changing a glossary.

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

1. Challenge terms that conflict with the glossary; let the user choose the canonical meaning or name.
2. For fuzzy or overloaded language, propose one `**Term**: definition` and optional `_Avoid_:` names.
3. Stress-test fuzzy relationships with concrete edge-case scenarios that force their boundaries to become explicit.
4. Cross-check claims against source and surface contradictions as questions rather than silently encoding them.
5. Update resolved terms immediately in the relevant `domain/**/CONTEXT.md`.
6. Offer ADRs only at the threshold above and link created ADRs from the active plan or dream.

Done when each resolved term has one definition, each changed decision has reciprocal supersession links, and material claims have durable evidence.
