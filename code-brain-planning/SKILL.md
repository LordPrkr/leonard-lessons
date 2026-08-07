---
name: code-brain-planning
description: "Durable Code Brain planning and execution. Use when broad, risky, or cross-cutting work needs artifacts or execution state to persist across sessions."
---

# Code Brain Planning

Use this workflow for durable work with a clear implementation route. Use `/code-brain-wayfinder` first when material decisions still obscure that route. Use `pragmatic-plan` instead when one lightweight field note is enough and the work needs no board state, formal receipt, execution slices, or cross-session orchestration. Follow `/code-brain` for root resolution, repository identity, project ownership, and evidence, and `/code-brain-writeback` while producing activity artifacts.

The parent/orchestrator alone writes plan metadata, `AGENTS.md`, and `KANBAN.md`; subagents never update project navigation or workflow state. Code Brain vault files are not source-repository commits.

## Before planning

Assume the Code Brain project is initialized. If `VISION.md` does not exist, invoke `/code-brain` and complete project bootstrap before planning. Then scan `plans/` and create the next `plans/<NNN_TOPIC>/` folder. Add its `plan.md` to `AGENTS.md` under Active plans, and move its existing board card to In Progress or create one there.

Read [`references/TEMPLATE.md`](./references/TEMPLATE.md) before writing `plan.md`. Apply `/code-brain`'s plan authoring contract for frontmatter and status management, replace every placeholder, and omit inapplicable evidence, references, and optional siblings. Link every created sibling and relevant ADR with relative Markdown links. Create `notes.md` and optional artifacts only when useful.

Capture each affected source repository's full `HEAD` independently before implementation. Do not modify a repository with unrelated staged or unstaged work unless the user explicitly approves that boundary.

## Lifecycle

The board lane is workflow state; the plan authoring contract owns the shared frontmatter and design-status lifecycle. The table below maps that status to this workflow's Kanban lanes and machine edges.

| Event | Plan status | Kanban lane | Machine edge |
| --- | --- | --- | --- |
| Untriaged task captured | no plan | Inbox | outside machine |
| Plan folder created / drafting | `draft` | In Progress | `context-ready` → `draft_plan` |
| Plan sent for adversarial review | `draft` | Review | `draft-ready` → `review_plan` |
| Review requires changes | `draft` | In Progress | `changes-needed` → `draft_plan` |
| Plan ready for user decision | `draft` | Review | `plan-ready` → `approval_gate` |
| User approves | `approved` | Ready | `user-approved` → `approved_ready` |
| User requests substantive revision before implementation | `draft` | In Progress | `revision-requested` → `draft_plan` |
| Implementation starts from Ready | `approved` | In Progress | `start-implementation` → `implement` |
| Recovery retries unchanged plan | `approved` | In Progress | `retry-approved-plan` → `implement` |
| Implementation reaches review | `approved` | Review | `implementation-ready` → `review_implementation` |
| Review finds approved fixes | `approved` | In Progress | `fixes-needed` → `apply_fixes` |
| Implementation or review cannot continue | `approved` | Blocked | `blocked` → `persist_receipt` |
| Attempt is partial | `approved` | Blocked | `partial` → `persist_receipt` |
| Delivered implementation is reverted | `approved` | Blocked | `reverted` → `persist_receipt` |
| Review accepts delivery | `approved` | Review | `accepted` → `finalize_implementation` |
| Accepted receipt persisted | `implemented` | Done | `receipt-accepted` → `done` |
| Blocked/partial/reverted receipt persisted | `approved` | Blocked | matching receipt edge → `await_recovery` |
| User abandons work | `abandoned` | Done | `abandon` → `done` |
| User replaces plan | `superseded` | Done | `supersede` → `done` |
| Recovery changes design | `draft` | In Progress | `revise-plan` → `draft_plan` |
| User pauses blocked work | `approved` | Blocked | `pause` → end |

For abandonment or supersession, retain the card in Done with `— abandoned` or `— superseded`; the linked plan carries canonical status. Remove implemented, abandoned, and superseded plans from `AGENTS.md`; approved Blocked plans remain active.

## Steps

### 1. Build context

Use bounded local reconnaissance and external research only when it materially affects the plan. Apply `/code-brain-writeback` with findings in `notes.md` and reusable-candidate pointers under `Documentation candidates`. Invoke `domain-modeling` when planning resolves domain language or an ADR-worthy decision.

Done when every likely touchpoint, constraint, material source, and unresolved decision is explicit, and every useful finding is already present in `notes.md`.

### 2. Challenge direction

Use a read-only second opinion for an irreversible migration, external contract change, ownership or security boundary, unresolved architectural choice, or cross-repository coordination. Accept or reject recommendations before drafting; otherwise record that none of these triggers applies.

Done when each directional decision is explicit and every review trigger is handled or explicitly absent.

### 3. Draft and review

Apply `/code-brain`'s plan authoring contract.

For work that exceeds one fresh worker context, add execution slices that each deliver observable behavior, reference their implementation steps, acceptance criteria, blockers, and verification; otherwise omit them. Work unblocked slices first. For a wide mechanical migration, use explicit expand–migrate–contract slices instead of forcing a false vertical delivery. Move the card to Review through the lifecycle table's `draft-ready` transition. The read-only plan reviewer must use only the plan and apply `/spellbinding-sentences`, including its referent check. Incorporate accepted findings into the current standalone plan. Use the table's `changes-needed` transition while editing.

Done when the plan satisfies `/code-brain`'s plan authoring contract, the reviewer confirms that every project-specific phrase has a recoverable referent without relying on prior conversation, each required slice is observable, blocker-aware, and fits one fresh context, and the card is in Review awaiting a user decision.

### 4. Approval gate

Present the plan and wait. Explicit approval changes only `status` to `approved` and moves the card to Ready; it does not start implementation. Before implementation, requested substantive changes restore `draft`, In Progress, review, and this gate. An implemented plan remains unchanged; later work starts a new plan.

Done when the approved plan is Ready or work ends explicitly.

### 5. Implement and review

Use the lifecycle table's `start-implementation` transition to move an approved Ready card to In Progress. Invoke `/feature-branch` in each affected source repository before spawning workers. For each unblocked execution slice, spawn exactly one `worker` with `context: "fresh"`; a plan without slices is one slice. Its task contains only an instruction to invoke `/effective-engineer`, the approved `plan.md` path, and the slice identifier. The worker returns changed files, command exit codes, validation evidence, deviations, residual risks, and blockers. The parent remains the sole writer of plan metadata and board state.

Use the lifecycle table's `implementation-ready` transition when implementation reaches review. Read-only reviewers check every acceptance criterion against the delivered source, then check correctness, validation, simplicity, and repository standards. Apply accepted fixes through `fixes-needed`, then return through `implementation-ready`. A blocked, partial, or reverted result follows its matching table transition and persists the attempt receipt immediately.

Done when every acceptance criterion is accounted for and review accepts delivery, or an honest non-accepted receipt is required.

### 6. Finalize implementation and receipt

Read [`references/RECEIPT.md`](./references/RECEIPT.md). Create `receipt.md` once, add `[Implementation receipt](./receipt.md)` to the plan's References, and append one chronological section after every attempt; frontmatter always reflects the latest attempt.

For accepted work, invoke `/finalize-implementation` in every changed source repository before persisting evidence. Record each resulting full commit SHA and `none` as its change-set hash. Never identify pre-change `HEAD` as delivered source and never claim the non-Git vault was committed. If finalization cannot complete, persist the actual committed or uncommitted evidence, leave plan status `approved`, and move the card to Blocked.

For blocked, partial, or reverted work, immediately record every affected repository's base SHA, `uncommitted`, and complete change-set hash. Leave plan status `approved` and the card Blocked. Recovery may retry the unchanged design, revise it through draft/review/approval, abandon, supersede, or pause.

Only after accepted evidence covers every changed repository and finalization succeeds, set `status: implemented` and move the card to Done.

Done when `receipt.md` contains the appended attempt, every changed repository has source evidence, and plan status plus Kanban lane match the accepted or non-accepted outcome.
