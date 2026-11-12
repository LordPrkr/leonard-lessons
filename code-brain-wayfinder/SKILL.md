---
name: code-brain-wayfinder
description: "Chart and resolve an uncertain, multi-session effort as decision tickets in the project's configured issue tracker."
disable-model-invocation: true
---

# Code Brain Wayfinder

Use this when the destination is clear but material decisions block a single plan; it resolves decisions and delivers no features. Follow `$code-brain` for project conventions and the confirmed tracker workflow, and use [the formats](./references/FORMATS.md) for maps and tickets.

## 1. Chart the map

Agree with the user on the destination (what becomes possible, not how), then write `wayfinding/<NNN_TOPIC>/map.md` with a ticket note and linked tracker issue for each precise question. Record vaguer uncertainty as Fog and exclusions as Out of Scope.

Done when every ticket links one issue and the first unblocked tickets are known.

## 2. Work one ticket

Claim the next unblocked ticket and resolve it by type: grill the user one question at a time, research primary sources, prototype disposably (removing prototype code afterwards), or do the narrow task that unblocks it. Record the resolution and evidence in the ticket, add a one-line gist to the map's Decisions, and close its issue.

Done when the ticket is resolved, its issue is closed, and newly precise fog has become tickets.

## 3. Hand off

Once every ticket is resolved or cancelled, choose the next session's route—`$code-brain-slicing` if a tracker project or stories are still needed, otherwise `$code-brain-planning` for the agreed first slice—and record it in the map's Outcome. Invoke `$handoff` with only that route's instructions and the repository, base, and map paths, then report its path and stop.

Done when the handoff names exactly one entry skill, and no slicing or planning has started in this session.
