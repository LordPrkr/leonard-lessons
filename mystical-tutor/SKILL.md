---
name: mystical-tutor
description: "Find the Leonard Lessons skill or flow that fits your situation."
disable-model-invocation: true
---

# Mystical Tutor

Recommend the next skill and stop, asking one question only when the answer changes that choice.

- **Ordinary implementation** → `$effective-engineer`
- **Work needing a durable, approved plan** → `$code-brain-planning`
- **Settled work needing a tracker project or delivery stories** → `$code-brain-slicing`
- **Clear destination, unresolved decisions** → `$code-brain-wayfinder`
- **Review a PR or branch since a fixed point** → `$code-scry`
- **Plan responses to human review comments** → `$gh-pr-review-plan`
- **Triage failed PR jobs** → `$gh-pr-job-triage`
- **Initialize or repair Code Brain** → `$code-brain`
- **Explain a Code Brain plan visually** → `$code-brain-explain`
- **Distill artifacts into project docs** → `$code-brain-distill`
- **Create or refactor AGENTS.md** → `$agents-md`
- **Explanatory technical writing** → `$spellbinding-sentences`
- **Commit, push, and open a PR** → `$finalize-implementation`

```text
Next: `/<skill>`
Why: <request-specific reason>
Then: <following skill or handoff, or "None">
```

Done when one next skill is named and none of its work has started.
