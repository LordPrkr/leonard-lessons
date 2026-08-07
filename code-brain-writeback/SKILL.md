---
name: code-brain-writeback
description: "Write through Code Brain findings. Use when another skill must persist exploration, planning, or review findings as they emerge."
---

# Code Brain Writeback

Write through material findings to the caller's activity artifact as they emerge. Follow `/code-brain` for repository identity and evidence. The calling skill supplies the artifact path, findings section, reusable-candidate section, and lifecycle.

A finding is material when it changes scope, design, classification, or recommendation; resolves uncertainty; establishes a reusable pattern; or would be costly to rediscover.

## Rules

- Create the activity artifact no later than the first material finding.
- Persist each material finding with its evidence and applicability boundary before the next exploratory or assessment tool call.
- Update the existing entry when later evidence sharpens or disproves it; keep the current conclusion rather than revision residue.
- Keep routine listings, transient dead ends, guesses, and task status out of findings.
- For a finding reusable beyond the current activity, add one pointer to its supporting finding under the reusable-candidate section supplied by the caller. Promotion belongs to `/code-brain-distill`.
- Persist the exact current plan, review, recommendation, or outcome before presenting it. While the caller's lifecycle permits revision, replace superseded generated sections instead of appending copies. Preserve immutable artifacts unchanged; for an implemented plan, write later material to the new artifact required by the caller's lifecycle.

**Complete when:** every material finding is accounted for in the caller's findings section and every reusable candidate points from the caller's declared candidate section to its supporting finding.
