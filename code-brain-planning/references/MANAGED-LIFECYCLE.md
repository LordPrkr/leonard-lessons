# Managed lifecycle

Read this only after `code-brain-planning` selects **Managed**. The board lane is workflow state; `/code-brain` owns shared frontmatter and design status.

| Event | Plan status | Kanban lane |
| --- | --- | --- |
| Plan folder created / drafting | `draft` | In Progress |
| Plan sent for review | `draft` | Review |
| Review requires changes | `draft` | In Progress |
| Plan ready for user decision | `draft` | Review |
| User approves | `approved` | Ready |
| Implementation starts | `approved` | In Progress |
| Implementation reaches review | `approved` | Review |
| Review finds accepted fixes | `approved` | In Progress |
| Implementation, review, or finalization is blocked or partial | `approved` | Blocked |
| Review accepts and receipt is persisted | `implemented` | Done |
| User abandons or replaces work | `abandoned` or `superseded` | Done |

## Managed creation

Add `plan.md` to `AGENTS.md` under Active plans. Move an existing card to In Progress or create it there. For abandonment or supersession, retain the card in Done with the terminal label. Remove implemented, abandoned, and superseded plans from `AGENTS.md`; approved Blocked plans remain active.

## Managed review and execution

Use execution slices only when work exceeds one fresh worker context. Each slice delivers observable behavior and names its implementation steps, acceptance criteria, blockers, and verification. Work unblocked slices first; wide mechanical migrations may use explicit expand–migrate–contract slices.

Move the card to Review after drafting. The read-only reviewer checks the standalone plan, including whether every project-specific phrase has a recoverable referent. After approval, move the card to Ready; implementation starts only when it moves to In Progress. A blocked, partial, or reverted result moves to Blocked and persists its receipt immediately.

## Receipt

Read [`RECEIPT.md`](./RECEIPT.md) before recording an attempt. Create `receipt.md` once, link it from `plan.md`, and append one chronological section after every attempt; frontmatter reflects the latest attempt.

For accepted work, record each changed repository's full delivered commit SHA and `none` as its change-set hash. For blocked, partial, or reverted work, record every affected repository's base SHA, `uncommitted`, and complete change-set hash. Never identify pre-change `HEAD` as delivered source. Only after accepted evidence covers every changed repository and finalization succeeds, set `status: implemented` and move the card to Done.
