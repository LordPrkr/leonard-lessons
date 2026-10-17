---
date: "<YYYY-MM-DD>"
status: draft
---

# <Plan title>

## Problem

<One or two concise sentences about the problem.>

## Goal

<One or two concise sentences about the desired outcome.>

## Context

<One or two concise sentences summarizing the user's specific ask.>

## Precedent

<Source paths and symbols @ full revision, why each applies, and the patterns to reuse. Link supporting artifacts here when relevant.>

## Deviations

<Necessary departures and authorization or requested decisions, using the Follow precedent disclosure fields; record conflicts and search gaps, or "None.">

## Files

```diff
 <repository>/
/├── <changed-file>
+├── <added-file>
-└── <deleted-file>
```

## Implementation

### Added

```diff
+// <Intended behavior and reason.>
+<top-level definition signature or name>
```

### Changed

```diff
-// <Current behavior.>
-<current top-level definition signature or name>
+// <Proposed behavior and reason.>
+<proposed top-level definition signature or name>
```

### Deleted

```diff
-// <Reason for removal.>
-<top-level definition signature or name>
```

<!-- Omit empty definition groups. -->

## Execution Slices

<!-- Managed only; omit when the plan fits one implementation subagent's fresh context. -->

1. **<Slice title>** — delivers <observable behavior>; definitions <names from Implementation>; blocked by <slices or None>; test strategy <corresponding checks below>.

## Test Strategy

- <Change or behavior> — <existing test seam, command, or manual check; explain when automated tests are unwarranted.>

## Questions

- <Open question, or "None.">
- ~~<Answered question>~~ Answer: <Answer established in chat and reflected in the plan.>

## Outcome

<Leave empty until implementation; then record delivery, checks performed, deviations, residual risks, and blockers. For managed work, link receipt.md here.>
