---
name: code-brain-dispatch
description: "Launch and coordinate T3 Code threads for ready delivery tickets after Code Brain slicing, handing off each newly unblocked ticket as its dependencies finish."
---

# Code Brain Dispatch

This thread coordinates the slice graph and launches one T3 Code thread per ready story; ticket threads own planning and delivery. Follow `$code-brain` for project conventions and the confirmed tracker workflow.

## 1. Resolve the graph

Fetch the slice index's stories, status, owners, and blocking links from the tracker. A story is ready when every prerequisite is complete under the tracker's rules and integrated into the delivery base—an open PR or `implemented` plan is not enough.

Done when ready, owned, and blocked stories are each known, with blockers named.

## 2. Reconcile ownership

Keep a coordinator record (ticket, handoff path, thread link, PR) in the OS temp directory and report its path. Before launching, list existing T3 threads and reuse any thread already assigned to the ticket.

Done when no ready story would get a second thread.

## 3. Launch

For each unowned ready story, launch a thread with `t3_thread_launch` titled with the ticket ID, using `workspaceStrategy: {type: "worktree"}` on the verified base revision. The message links the issue, slice index, base, and conversation-only decisions, then includes the ticket brief below.

```md
Work only on <ticket> in this worktree. Invoke `$code-brain-planning` now, keeping its plan-approval gate, and use `$feature-branch` in this checkout. Report blockers here, link any PR you push, and finish with the plan and receipt paths, PR URL and head SHA, review results, and integration state. Leave sibling tickets to the coordinator.
```

Done when each launched thread's link is recorded and shown to the user verbatim.

## 4. Advance

On each completion notification or explicit resume, refresh the tracker graph and launch every newly ready story; hold dependents of failed or blocked work. When no notification covers the next transition, tell the user what event to resume on.

Done when the frontier is launched, queued, or blocked, and the effort is complete only when every in-scope story meets its tracker completion rule.
