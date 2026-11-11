---
name: code-brain-dispatch
description: "Launch and coordinate T3 Code threads for ready delivery tickets after Code Brain slicing, handing off each newly unblocked ticket as its dependencies finish."
---

# Code Brain Dispatch

Turn a published slice graph into fresh T3 Code threads, one per ready story. The current thread coordinates the graph; ticket threads own planning and delivery. Invoking this skill authorizes those ticket threads within the selected effort. Creating this skill or discussing dispatch does not start an effort.

Use `$code-brain` for repository identity, project context, and the confirmed tracker workflow. This skill writes its own handoffs using the conventions below; external `$handoff` is not required.

## 1. Resolve the graph

Read the supplied slice index, its tracker project, project `AGENTS.md`, `ISSUE_TRACKER.md`, and relevant domain context and ADRs. Resolve the source repository and T3 project before launching. When the effort is ambiguous, ask which index or project to dispatch. Incomplete slicing returns to `$code-brain-slicing`.

Fetch the scoped stories, their current status, owners, blocking relationships, and linked plans and PRs through the configured tracker tools. Include prerequisites outside the project when determining readiness; dispatch only stories inside the selected scope. Related issues and parent/child grouping are not blocking edges unless the tracker workflow defines them that way.

A **ready leaf** is an unfinished, available story whose blocking prerequisites are all satisfied under the confirmed tracker completion rules. This definition is independent of the tracker's edge direction. An unknown or unresolved prerequisite blocks readiness. A completed agent run, an `implemented` plan, or an open PR alone does not satisfy a prerequisite; verify required integration into the selected base as well. Preserve externally owned and in-progress work.

Check for cycles and missing dependency access. Hold affected stories and explain the blockers; independent ready stories can proceed. Use the user's concurrency limit when supplied, otherwise dispatch all ready stories within actual T3 capacity. Queue excess work without inventing a new limit. Establish the delivery base from the effort or repository default; use integrated prerequisites by default, and stacked branches only when explicitly requested.

Done when the scoped graph, completion rule, base, ready stories, existing owners, and blockers are known from current evidence.

## 2. Reconcile ownership

Keep a compact coordinator record in the OS temporary directory, outside the source checkout. Record the repository and T3 project identities, slice index, selected scope and base, concurrency choice, and each ticket's handoff path, launch attempt, thread ID/link, and PR references. Report its absolute path. It is a routing record; the tracker remains authoritative for status and dependencies.

On a resumed or repeated invocation, read the existing record and list T3 project threads, paging as needed. Match by canonical ticket ID and repository/project identity, then read candidate threads before deciding whether to reuse them. Also recheck tracker ownership. Reuse an existing ticket thread, including one waiting for approval; a failed, cancelled, or interrupted thread requires reconciliation, not automatic replacement. If ownership remains uncertain, hold that ticket and report it.

Use one coordinator for the selected effort. If another coordinator is active, resume it or obtain an explicit transfer before launching. Immediately before each launch, refresh readiness and ownership. Record the pending attempt first; reconcile ambiguous launch results before retrying.

Done when every candidate is either unowned and ready, assigned to a known thread or external owner, queued for capacity, or held with a specific reason.

## 3. Prepare and launch each handoff

For each unowned ready ticket, write a unique handoff document in the OS temporary directory and report its absolute path. Include:

- The one ticket's URL/ID, intended outcome, source repository and T3 project, slice index, and selected base.
- Links or paths to canonical acceptance criteria, dependencies, specifications, decisions, domain context, and any existing plan. Reference existing artifacts rather than copying their bodies.
- Conversation-only decisions and constraints needed to continue, with sensitive information redacted.
- Verified prerequisite completion and integration evidence, current blockers, and exact authorization already given. Backlog approval does not approve an implementation plan or a merge.
- A **Suggested skills** section directing the receiving agent to invoke `$code-brain-planning` for this ticket, with `$code-brain` for shared context. An existing plan is an input to that workflow; verify its applicability and approval before implementation.
- The receiving contract in [Ticket thread contract](./references/TICKET-THREAD.md).

Refresh the selected delivery base before launch, resolve the actual starting commit, and verify that required prerequisite changes are included in that revision. Fetch the remote base when applicable; hold the ticket if the available base lacks those changes. Record that revision in the handoff.

Discover the actual T3 tool schemas. Use `t3_thread_launch` for a new top-level ticket thread, passing the handoff in `message`. Include the document's text as well as its absolute path so continuation survives temporary-file loss. Use a title containing the canonical ticket ID. Set `workspaceStrategy` to `type: "worktree"` with the verified revision as `baseRef` and a ticket-specific branch; let T3 provision and bind the checkout before the agent starts. Inherit provider, model, options, interaction mode, and runtime permissions unless the user specifies otherwise. No shell-created checkout or checkout-setup prompt is needed.

Persist the returned identity immediately, then call `t3_thread_read` or `t3_thread_wait` as required by the launch tool. Present the returned thread `link` verbatim; if absent use `[title](t3-thread://v1/<exact thread ID>)`. On an error or lost reply, list and read matching threads before any retry. If launch is unavailable, retain the prepared documents and report the capability gap rather than silently substituting subagents or another app.

Done when every dispatchable ticket has exactly one reconciled T3 thread with its handoff, or a retained handoff and explicit launch blocker.

## 4. Advance the frontier

Use T3's supported completion notifications and `t3_thread_wait` to resume coordination. Follow a returned `next` instruction, including ending the turn when completion will wake it; avoid polling loops. A thread awaiting plan approval retains its assignment and needs user attention in that thread.

On each completion notification, tracker update supplied by the user, or explicit resume, read the relevant ticket threads and refresh the tracker graph and prerequisite integration evidence. Reconcile the record, then repeat ownership checks and dispatch for **every newly ready leaf**, including joins that require several prerequisites. A failed or blocked ticket holds its dependents while independent work continues. Cancellation or reopening removes completion assumptions; hold affected unlaunched work and notify already running dependents of the changed prerequisite.

Keep dispatch in the coordinator: ticket threads report results and never recursively dispatch siblings or successors. Obey the host's PR watch requirements when waiting on checks or reviews. If no supported notification covers the next dependency transition, report the exact event needed and how to resume with this skill and its coordinator record. Do not promise unattended progression or install a recurring schedule without the user's request.

Done when the current frontier is assigned, queued, or explicitly blocked, the coordinator record is updated, and the next wake or manual resume condition is clear. The effort is complete only when the tracker and integration evidence confirm every in-scope story meets its completion rule; an empty ready set alone is insufficient.
