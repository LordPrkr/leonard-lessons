---
name: code-brain-planning
description: "Durable Code Brain planning and execution. Use when broad, risky, or cross-cutting work needs artifacts or execution state to persist across sessions."
---

# Code Brain Planning

Use this workflow for durable work. Use `pragmatic-plan` instead for a lightweight in-session plan with no Code Brain artifacts. Follow `/code-brain` for root resolution, repository identity, project ownership, and evidence.

The parent/orchestrator alone writes plan metadata, `AGENTS.md`, and `KANBAN.md`; subagents never update project navigation or workflow state. Code Brain vault files are not source-repository commits.

## Before planning

Assume the Code Brain project is initialized. If `VISION.md` does not exist, invoke `/code-brain` and complete project bootstrap before planning. Then scan `plans/` and create the next `plans/<NNN_TOPIC>/` folder. Add its `plan.md` to `AGENTS.md` under Active plans, and move its existing board card to In Progress or create one there.

Read [`references/TEMPLATE.md`](./references/TEMPLATE.md) before writing `plan.md`. Set its creation date and `status: draft`, replace every placeholder, and omit inapplicable evidence, references, and optional siblings. Link every created sibling and relevant ADR with relative Markdown links. Create `notes.md` and optional artifacts only when useful.

Capture each affected source repository's full `HEAD` independently before implementation. Do not modify a repository with unrelated staged or unstaged work unless the user explicitly approves that boundary.

## Lifecycle

The board lane is workflow state; plan frontmatter is design lifecycle. New plans use `draft`, `approved`, `implemented`, `abandoned`, or `superseded`. Only explicit user approval sets `approved`. Any substantive design revision returns the plan to `draft`, reruns review, and waits for approval. Read legacy `approved:` through `/code-brain`'s mapping but never write it.

| Event | Plan status | Kanban lane | Machine edge |
| --- | --- | --- | --- |
| Untriaged task captured | no plan | Inbox | outside machine |
| Plan folder created / drafting | `draft` | In Progress | `context-ready` → `draft_plan` |
| Plan sent for adversarial review | `draft` | Review | `draft-ready` → `review_plan` |
| Review requires changes | `draft` | In Progress | `changes-needed` → `draft_plan` |
| Plan ready for user decision | `draft` | Review | `plan-ready` → `approval_gate` |
| User approves | `approved` | Ready | `user-approved` → `approved_ready` |
| User requests substantive revision | `draft` | In Progress | `revision-requested` → `draft_plan` |
| Implementation starts from Ready | `approved` | In Progress | `start-implementation` → `implement` |
| Recovery retries unchanged plan | `approved` | In Progress | `retry-approved-plan` → `implement` |
| Implementation reaches review | `approved` | Review | `implementation-ready` → `review_implementation` |
| Review finds approved fixes | `approved` | In Progress | `fixes-needed` → `apply_fixes` |
| Implementation or review cannot continue | `approved` | Blocked | `blocked` → `persist_receipt` |
| Attempt is partial | `approved` | Blocked | `partial` → `persist_receipt` |
| Delivered implementation is reverted | `approved` | Blocked | `reverted` → `persist_receipt` |
| Review accepts delivery | `approved` | Review | `accepted` → `commit_decision` |
| Accepted receipt persisted | `implemented` | Done | `receipt-accepted` → `done` |
| Blocked/partial/reverted receipt persisted | `approved` | Blocked | matching receipt edge → `await_recovery` |
| User abandons work | `abandoned` | Done | `abandon` → `done` |
| User replaces plan | `superseded` | Done | `supersede` → `done` |
| Recovery changes design | `draft` | In Progress | `revise-plan` → `draft_plan` |
| User pauses blocked work | `approved` | Blocked | `pause` → end |

For abandonment or supersession, retain the card in Done with `— abandoned` or `— superseded`; the linked plan carries canonical status. Remove implemented, abandoned, and superseded plans from `AGENTS.md`; approved Blocked plans remain active.

## Steps

### 1. Build context

Use bounded local reconnaissance and external research only when it materially affects the plan. Persist useful findings in `notes.md`. Apply `/code-brain` evidence conventions to source-backed or external claims. Invoke `domain-modeling` when planning resolves domain language or an ADR-worthy decision.

Done when every likely touchpoint, constraint, material source, and unresolved decision is explicit.

### 2. Challenge direction

Use a read-only second opinion when assumptions, architecture, scope, or trajectory need it. Accept or reject recommendations before drafting.

Done when no directional decision is implicit.

### 3. Draft and review

Write a standalone worker handoff with problem, goal, out-of-scope boundary, context, observable acceptance criteria, exact files, the highest existing public test seam, one red-green step per observable behavior, important end-state snippets, tests, verification, risks, questions, and artifact links. For work that exceeds one fresh worker context, add execution slices that each deliver observable behavior, reference their implementation steps, acceptance criteria, blockers, and verification; otherwise omit them. Work unblocked slices first. For a wide mechanical migration, use explicit expand–migrate–contract slices instead of forcing a false vertical delivery. Do not leave conditional implementation branches. Move the card to Review for adversarial review, then incorporate accepted findings without revision-history residue. Changes return the card to In Progress while editing.

Done when a fresh worker can execute the plan, the problem and scope boundary are explicit, every acceptance criterion is covered by its implementation and verification, each required slice is observable, blocker-aware, and fits one fresh context, and the card is in Review awaiting a user decision.

### 4. Approval gate

Present the plan and wait. Explicit approval changes only `status` to `approved` and moves the card to Ready; it does not start implementation. Requested substantive changes restore `draft`, In Progress, review, and this gate.

Done when the approved plan is Ready or work ends explicitly.

### 5. Implement and review

Only `start-implementation` moves an approved Ready card to In Progress. Implement unblocked execution slices with a fresh worker; a plan without slices is one slice. Give each worker the approved plan, its slice, acceptance criteria, verification commands, base revisions, and a required handoff containing changed files, command exit codes, validation evidence, deviations, residual risks, and blockers.

Move the card to Review when implementation is ready. Read-only reviewers check every acceptance criterion against the delivered source, then check correctness, validation, simplicity, and repository standards. Approved fixes return it to In Progress and then Review. If implementation or review is blocked, partial, or reverted, skip commits and persist the attempt receipt immediately.

Done when every acceptance criterion is accounted for and review accepts delivery, or an honest non-accepted receipt is required.

### 6. Commit decision and receipt

Read [`references/RECEIPT.md`](./references/RECEIPT.md). Create `receipt.md` once, add `[Implementation receipt](./receipt.md)` to the plan's References, and append one chronological section after every attempt; frontmatter always reflects the latest attempt.

For accepted work, ask whether the user authorizes source commits, naming every changed repository. Commit only explicitly authorized repositories, before persisting accepted evidence. Record the resulting full commit SHA and `none` as its change-set hash. For each repository left uncommitted, record `uncommitted` and the deterministic complete change-set hash. Never identify pre-change `HEAD` as delivered source and never claim the non-Git vault was committed.

For blocked, partial, or reverted work, immediately record every affected repository's base SHA, `uncommitted`, and complete change-set hash. Leave plan status `approved` and the card Blocked. Recovery may retry the unchanged design, revise it through draft/review/approval, abandon, supersede, or pause.

Only after accepted evidence covers every changed repository set `status: implemented` and move the card to Done. A later authorized commit appends a commit-finalization entry and updates that repository's evidence row without rewriting the earlier attempt body.

Done when `receipt.md` contains the appended attempt, every changed repository has source evidence, and plan status plus Kanban lane match the accepted or non-accepted outcome.
