---
name: tracer-bullet
description: >-
  Tracer bullet prototype workflow. Use when the user gives a plan and wants to
  prove technical feasibility, spike implementation details, or fire a
  disposable end-to-end path before committing to the full build.
---

# Tracer Bullet

Create a disposable prototype from the plan to prove technical feasibility and
expose implementation details. This is a spike, not the final feature: prefer
the shortest end-to-end path, hardcode safe values, skip polish, and keep the
diff easy to delete.

Use `/code-brain` project folder conventions for all durable notes.

## Steps

### 1. Locate the Plan

Find the plan text from the prompt or Code Brain `plans/`. If the user names a
plan, search `~/Documents/Code Brain/<repo>/plans/` using `/code-brain` repo
resolution.

Done when you have the plan content, or you can name that no Code Brain plan
file exists and will reference only the prompt plan.

### 2. Fire the Tracer Bullet

Build the smallest disposable prototype that exercises the risky path named by
the plan. Reuse existing code and installed dependencies; add no new dependency
unless the prototype cannot run without it. Mark prototype-only code with
`tracer-bullet:` comments or keep it on an isolated branch/file so deletion is
obvious.

Done when the prototype runs far enough to prove or disprove the technical path
and records the concrete files, APIs, commands, errors, and decisions
encountered.

### 3. Verify the Path

Run the smallest command that demonstrates the tracer bullet. Prefer an existing
targeted script, test, or manual command over new test scaffolding.

Done when the command result is captured, including any failure that proves
infeasibility or names the next blocking unknown.

### 4. Write Findings

Invoke `/code-brain`, then write `notes/<TOPIC> Tracer Bullet.md` with:

- link to the plan file when one exists; otherwise paste the prompt plan at
  the top
- goal and scope of the tracer bullet
- prototype location and how to run it
- findings: what worked, what failed, implementation details discovered
- recommendation: keep going, change plan, or stop
- cleanup list for disposable code

Done when the note exists in Code Brain `notes/` and either links back to the
plan file or includes the prompt plan at the top.
