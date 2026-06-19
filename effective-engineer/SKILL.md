---
name: effective-engineer
description: "Tight implementation loop for non-trivial code changes: inspect, test, implement, verify, summarize. Use when changing code unless the user asks for Code Brain planning, durable design artifacts, or approval-first execution."
---

# Effective Engineer

Use the tight loop. Escalate to `code-brain-planning` only when the change is broad, risky, cross-cutting, or the user asks for a plan/design artifact.

## Steps

### 1. Inspect

Read the smallest set of files needed to understand the change.

Done when you can name the files/functions to change, or you have one focused clarification question that blocks work.

### 2. Invoke `/tdd`

For non-trivial logic, invoke `/tdd` before implementation. Skip only for trivial wiring, docs, or mechanical edits.

Done when `/tdd` has produced a failing test for the intended reason, or the skip reason is explicit.

### 3. Implement

Make the smallest code change that satisfies the request and the test. Do not add abstractions for future cases.

Done when the requested behavior is implemented with the shortest maintainable diff.

### 4. Verify

Run the smallest relevant check: targeted test first, then typecheck/lint only when touched code needs it or the repo makes it cheap.

Done when checks pass, or any remaining failure is unrelated and named.

### 5. Summarize

Report changed files and verification.

Done when the user can see what changed and what was run.
