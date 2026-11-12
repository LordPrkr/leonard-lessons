---
name: effective-engineer
description: "Use for direct code changes or implementation delegated from an approved plan."
---

# Effective Engineer

Invoke `$feature-branch` before editing, and ask the user before anything needing credentials, private-registry access, an unexpected lockfile change, a destructive command, or a departure from the approved plan.

## 1. Implement

Implement the request with the smallest diff and the tests that applicable precedent expects.

Done when the behavior and its tests exist.

## 2. Verify

Run targeted checks, then the repository-mandated aggregate checks proportionate to the blast radius.

Done when required checks pass, or a blocker is reported with the failed command and the decision needed.

## 3. Deliver

Invoke `$finalize-implementation`.
