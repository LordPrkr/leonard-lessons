# Ticket thread contract

Include these instructions in each ticket's launch message along with its handoff context.

Work on the assigned ticket only, in the worktree bound by T3. Read the repository instructions, handoff references, canonical issue, and current prerequisites before planning. If readiness or the selected base is stale, report the discrepancy to the coordinator and hold affected work.

Invoke `$code-brain-planning` with the ticket and slice index. Preserve its review, explicit plan approval, implementation, review, and receipt requirements. The user-approved backlog authorizes the slice's scope; implementation still requires approval of its concrete plan. Continue an existing applicable plan through its remaining gates rather than duplicating it.

Parallel ticket threads share the Code Brain project. When allocating a new numbered plan folder, create it exclusively; if another thread claims that number first, rescan and choose the next number. Preserve other tickets' index and router links when writing shared artifacts.

Use the T3-provisioned checkout as the delivery workspace; apply `$feature-branch` to confirm and provision its dependencies without moving to a second checkout. Delegate the workers and reviewers required by planning, but keep them scoped to this ticket. Dispatching other graph tickets belongs to the coordinator.

Report blockers and approval requests in this thread. Follow the confirmed tracker workflow for ownership, status updates, and completion. Finalization or a plan receipt does not by itself establish integration or authorize merging. Link created or pushed PRs through the host's required PR-linking tool immediately.

Finish with the ticket reference, plan and receipt paths, delivery PR URL and head SHA, verification and review results, integration state, tracker updates, and remaining blockers. The coordinator uses this evidence to recheck the graph.
