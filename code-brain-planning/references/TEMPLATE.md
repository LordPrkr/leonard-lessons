---
date: "<YYYY-MM-DD>"
status: draft
---

# <Plan title>

## Goal

<The outcome this plan must deliver.>

## Context

<Current behavior, constraints, and evidence needed by a fresh-context worker.>

## Acceptance Criteria

- <Observable condition that must hold when the plan is complete.>

## Files

- `<path>` — <change and reason>

## Implementation

### 1. <Step name>

**Red:** <Test that fails for the intended reason.>

**Green:** <Smallest implementation that passes the test.>

<Important end-state code snippet, API shape, query, or component tree.>

## Execution Slices

<!-- Omit when the plan fits one fresh worker context. -->

1. **<Slice title>** — implementation steps <N–N>; acceptance criteria <items>; verify with `<command>`.

## Test Strategy

<Coverage required beyond the TDD steps.>

## Verification

```bash
<commands with expected outcomes>
```

## Risks

- <Risk and mitigation.>

## Questions

- <Question that must be answered before implementation, or "None.">

## Evidence

- repo: `relative/path.ts` @ `<full SHA>` — inspected YYYY-MM-DD
- external: <https://example.com/spec> — accessed YYYY-MM-DD

## References

- [Context notes](./notes.md)
- <Relevant Code Brain ADR or sibling artifact.>
