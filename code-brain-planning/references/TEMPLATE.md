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

<Brief summary of the patterns to reuse, referencing repository paths and definitions.>

## Deviations

<Necessary departures and authorization or requested decisions, using the Follow precedent disclosure fields; record conflicts and search gaps, or "None.">

## Files

```text
<repository>/
M ├── <changed-file>
A ├── <added-file>
D └── <deleted-file>
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

## Test Strategy

- <Change or behavior> — <existing test seam, command, or manual check; explain when automated tests are unwarranted.>

## Questions

- <Open question, or "None.">
- ~~<Answered question>~~ Answer: <Answer established in chat and reflected in the plan.>

## Outcome

<Leave empty until finalization; then link receipt.md.>
