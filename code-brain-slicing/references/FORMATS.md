# Project, Story, and Index Formats

## Scoped project brief

Publish this brief in the tracker's project description or configured equivalent. Adapt the fields to its confirmed conventions.

```md
# <Scoped delivery project name>

## Objective

<What becomes possible when this effort is delivered and who benefits.>

## Scope

- <Included capability or outcome.>

## Exclusions

- <Explicit boundary or deferral and why, or None.>

## Completion

<Observable conditions establishing that the scoped objective is delivered.>

## Evidence

- <Source goal, specification, wayfinding map, or decision reference.>
```

## Delivery story

Use one issue per story in the configured tracker. Adapt these sections to its confirmed issue conventions.

```md
# <Observable outcome>

## Story

<For product work: As a real beneficiary, I want a behavior, so that I gain a concrete benefit. For technical work: state the observable capability or operational outcome without inventing a persona.>

## Acceptance Criteria

1. <Given a relevant condition, the observable result that establishes success.>
2. <The observable result for a material failure or boundary case, when relevant.>

## Tasks

- [ ] <Delivery work contributing to named acceptance criteria.>

## Dependencies

- <Blocking story or prerequisite and why it gates this outcome, or None.>

## Evidence

- <Requirement, decision ticket, ADR, or inspected source supporting the story.>
```

Tasks describe delivery work; file-level design and test implementation belong to planning. Acceptance criteria define completion independently of whether the task checklist is checked off.

## Slice index

Store the index at the location selected by the skill's publication step. Reuse it for the same effort.

```md
# <Effort> Delivery Slices

## Goal

<One-line destination and link to the source goal, specification, or map.>

## Tracker Project

<Project name, URL or stable ID, and parent repository/team scope needed to locate it. The tracker holds the brief and membership.>

## Stories

<!-- Dependency order; each issue holds its story, acceptance criteria, and tasks. -->
1. [<Story title>](<issue URL>)

## First Slice

<Link to the recommended story and why it comes first, or the prerequisite preventing selection. Recheck availability in the tracker before planning.>

## Deferred Scope

- <Explicitly agreed deferral or exclusion and its reason, or None.>

## Evidence

- <Relative links to source requirements, map, decisions, and ADRs.>
```
