---
name: effective-engineer
description: "Use for direct code changes or implementation delegated from an approved plan."
---

# Effective Engineer

## Delivery

Invoke /feature-branch before changing implementation files.

Ask for help before proceeding when repair requires credentials or private-registry access, unexpectedly changes the lockfile or package source, needs a privileged or destructive command, or conflicts with the approved plan's design or scope.

Complete when: the work has a delivery owner and an independently provisioned workspace.

## Steps

### 1. Implement

Invoke /tdd

Done when the requested behavior is implemented with the smallest diff consistent with applicable precedent and authorized deviations.

### 2. Verify

Run targeted checks first, then repository-mandated aggregate checks or the full suite when feasible and proportionate to the blast radius.

Done when required checks pass, or a hard boundary has been escalated with the failed command, attempted repair, and smallest decision needed.

### 3. Deliver

Invoke $finalize-implementation
