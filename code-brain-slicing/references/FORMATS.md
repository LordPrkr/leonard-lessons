# Project, Story, and Index Formats

Adapt section names to the tracker's confirmed conventions.

## Project brief

```md
# <Project name>

## Objective
<What becomes possible and for whom.>

## Scope
- <Included outcome.>

## Exclusions
- <Boundary and why, or None.>

## Completion
<Observable conditions that mean the effort is delivered.>
```

## Story

```md
# <Observable outcome>

## Story
<"As a <beneficiary>, I want <behavior>, so that <benefit>", or the technical outcome.>

## Acceptance Criteria
1. <Given a condition, the observable result.>

## Tasks
- [ ] <Delivery work.>

## Dependencies
- <Blocking story and why, or None.>

## Evidence
- <Requirement, decision ticket, ADR, or source.>
```

## Slice index

```md
# <Effort> Delivery Slices

## Goal
<One line, linking the source goal or map.>

## Tracker Project
<Name and URL or stable ID.>

## Stories
1. [<Story title>](<issue URL>) — plan: <link once created>

## Deferred Scope
- <Deferral and reason, or None.>
```
