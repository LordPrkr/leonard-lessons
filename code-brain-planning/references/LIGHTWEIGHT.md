# Lightweight layout

Use this layout for a plan that fits one fresh worker and needs an approval gate, not managed coordination. Keep the shared frontmatter and every required element of `/code-brain`'s plan authoring contract, but place them under these four headings:

```md
---
date: YYYY-MM-DD
status: draft
---

# <Plan title>

## Exploration

<Observed flow, source evidence, and relevant constraints.>

## Documentation candidates

<Reusable candidate and evidence, or "None.">

## Plan

### Problem

### Goal

### Out of Scope

### Context

### Acceptance Criteria

### Files

### Implementation

### Test Strategy

### Verification

### Risks

### Questions

### Evidence

### References

## Outcome

<Leave empty until implementation; then record delivery, verification,
deviations, residual risks, and blockers.>
```

Do not add a board card, execution slices, receipt, or sibling note unless the work gains the coordination need that makes it Managed.
