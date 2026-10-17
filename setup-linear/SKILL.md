---
name: setup-linear
description: "Set up a repository's Linear team, project, and issue workflow before logging work."
---

# Setup Linear

Linear tracks work; `/code-brain` holds domain docs and durable project knowledge.

## 1. Fill the gaps

Resolve the project's `$CODE_BRAIN_ROOT/<repo>/` folder using `/code-brain`. Read existing project instructions and `ISSUE_TRACKER.md` in that folder. Use available Linear tools to identify the team, project, and existing statuses. Ask only for missing information: where issues belong and a short description of how this project creates, starts, reviews, and closes work, including how it handles blockers. Include assignment or other defaults only when the project requires them.

Done when the destination is unambiguous and the workflow names the existing statuses and when to use them. If Linear access is unavailable, ask for the connection needed to verify the setup.

## 2. Save the workflow

Write or update `$CODE_BRAIN_ROOT/<repo>/ISSUE_TRACKER.md`, alongside `VISION.md`, with the Linear team and project URLs or IDs and the workflow in plain prose. Add a relative link to it in that Code Brain project's `AGENTS.md`. Point domain-doc consumers to `/code-brain`. Preserve unrelated instructions and update existing pointers in place.

Report the resolved absolute path of every created artifact. The user can edit `ISSUE_TRACKER.md` directly as the workflow changes.

Done when the destination and statuses have been verified in Linear, the workflow contains enough information to create and update issues, and the Code Brain router link resolves.
