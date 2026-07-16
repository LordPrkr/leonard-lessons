---
name: tracer-bullet
description: >-
  Tracer bullet workflow. Use when a Code Brain plan or Wayfinder ticket needs
  a disposable end-to-end prototype to prove or disprove its risky technical path.
---

# Tracer Bullet

Build the shortest disposable path that proves or disproves a plan's technical risk. Use `/code-brain` for durable findings. A tracer is not the final feature.

## Steps

### 1. Locate the target and baseline

Resolve the repository and named Code Brain plan or Wayfinder ticket. If no durable target exists, retain the prompt target in the findings note. State one falsifiable question, the observable evidence that answers it, and what outcomes mean continue, revise, or stop.

Use an isolated Git worktree by default. If isolation is unavailable, do not edit until the existing working tree is clean. Before tracer work, capture the baseline branch, full `HEAD`, `git status --short`, tracked binary diff, and untracked paths.

Done when the question, decision threshold, plan, and isolation boundary are explicit and the baseline is saved outside the working tree.

### 2. Fire the tracer

Build the smallest end-to-end prototype for the risky path. Reuse existing code and dependencies; add a dependency only when the path cannot run without it. Mark prototype-only code with `tracer-bullet:` comments or keep it in isolated files so ownership is unambiguous.

Done when the prototype runs far enough to record concrete files, APIs, commands, failures, and decisions.

### 3. Verify and record findings

Run the smallest existing test, script, or manual command that proves the result. Write `notes/<TOPIC> Tracer Bullet.md` with the question, decision threshold, target link (or prompt target), scope, prototype location and command, findings, recommendation, and cleanup inventory. Link the findings from the plan or Wayfinder ticket.

If findings substantively change an approved plan, the parent sets its status back to `draft`, moves its card to In Progress, and sends the revised plan through review and approval again.

Done when evidence supports keep going, change plan, or stop.

### 4. Clean up exactly

Remove or restore only tracer-owned files and hunks. Never use broad restore or clean commands where pre-existing work could exist. Remove the isolated worktree and tracer branch when they were created solely for the spike.

Compare final branch, `HEAD`, status, tracked diff, and untracked paths with the captured baseline. Account for the durable Code Brain findings separately from source cleanup.

Done only when the source repository matches its baseline exactly or every intentional retained difference has the user's explicit approval.
