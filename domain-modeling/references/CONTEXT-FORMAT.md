# Glossary Format

A context file is a glossary of domain language, not a specification or implementation notebook.

```md
# <Bounded Context>

## Terms

**Order**: A confirmed request to purchase goods.
_Avoid_: cart, purchase record
```

Add a term only when it names a domain concept needed to understand the work. Keep definitions stable, concise, and free of code paths, database fields, framework types, or generic programming terms. Put a term in the context selected by `CONTEXT-MAP.md`; use the root `CONTEXT.md` only for a single-context project or a system-wide term.
