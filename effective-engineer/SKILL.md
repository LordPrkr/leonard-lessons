---
name: effective-engineer
description: "Implement code changes from applicable precedent through a tight inspect, test, implement, verify, and review loop. Use for direct changes or when another workflow delegates an approved plan."
---

# Effective Engineer

**Follow precedent.** Before inspecting or editing, read and apply [Follow precedent](follow-precedent.md). Its evidence and deviation requirements govern every step of this loop.

Use the tight loop. When executing an approved plan, treat it as the scope and implementation direction. Escalate unplanned broad, risky, or cross-cutting work to `code-brain-planning`.

## Delivery

Once the user approves implementation, own delivery through a reviewable pull request unless they explicitly request a local-only change. A parent workflow that explicitly owns delivery provisions the workspace and performs finalization; return reviewed implementation and evidence to that parent instead. For direct delivery, invoke `/feature-branch` before changing implementation files.

Ask for help before proceeding when repair requires credentials or private-registry access, unexpectedly changes the lockfile or package source, needs a privileged or destructive command, reveals a security concern, or conflicts with the approved plan's design or scope.

**Complete when:** the work has a delivery owner and an independently provisioned workspace, or the user has explicitly chosen local-only delivery.

## Steps

### 1. Inspect

Establish applicable precedent for the implementation and tests. Read the closest examples in the affected module, their callers, and existing tests. Cite paths and symbols for the helpers, validation owner, test seam, fixtures, setup and teardown, mocking, assertions, and verification commands you will reuse. Revalidate any precedent supplied by an approved plan against the implementation checkout.

Done when the files/functions to change and applicable implementation and test precedent are identified, with search gaps, conflicts, and necessary deviations disclosed under the shared contract; affected work waits only where direction is still required.

### 2. Invoke `/tdd`

For non-trivial logic, invoke `/tdd` at the highest existing public seam. Extend the closest tests in the same module using the cited fixtures, lifecycle, mocking, and assertion conventions. If that module has no applicable tests, establish the nearest applicable testing precedent before adding them. For each observable behavior: write one test, confirm it fails for the intended reason, add the minimum green implementation, then repeat. Skip only for trivial wiring, docs, or mechanical edits.

Done when each intended behavior has gone red then green at an established public seam using applicable test precedent or an authorized deviation, or the skip reason is explicit.

### 3. Implement

Adapt the cited implementation to satisfy the current red test. Keep each substantive choice within its applicable pattern or an authorized deviation.

Done when the requested behavior is implemented with the smallest diff consistent with applicable precedent and authorized deviations.

### 4. Verify

Run targeted checks first, then repository-mandated aggregate checks or the full suite when feasible and proportionate to the blast radius. Treat every failed validation as work to classify and resolve:

- Source failure: fix the implementation.
- Missing dependency, stale artifact, or project-graph failure: repair the current worktree with the repository-supported setup command, then rerun the check.
- CI or tool failure: reproduce it in a clean, provisioned checkout before classifying it as infrastructure.

Keep dependencies isolated to the worktree; validate source only against artifacts built for that same worktree. Escalate hard boundaries under **Delivery** rather than carrying an unverified failure forward.

Done when required checks pass, or a hard boundary has been escalated with the failed command, attempted repair, and smallest decision needed.

### 5. Review

Audit the complete diff against the cited implementation and test precedent, the request, authorized deviations, repository standards, correctness, and simplicity. When a pattern violation is found, inspect the complete change for other instances. Re-run affected checks after fixes.

Done when every substantive choice follows cited precedent or an explicitly authorized deviation and no actionable review finding remains.

### 6. Deliver or summarize

For direct delivery, invoke `/finalize-implementation` after review. For parent-owned delivery, return the changed files, verification, deviations, residual risks, and blockers to the parent. For local-only work, report the changed files and verification to the user.

Done when the delivery owner has the reviewed diff and verification evidence, or the user can see the local-only change and checks.
