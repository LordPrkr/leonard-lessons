---
name: technical-design-proposal
description: "Design proposal workflow for changes that cross API, runtime, security, compatibility, release, or operational boundaries. Use when proposing a system design, SDK capability, migration, integration, or deployment path."
---

# Technical Design Proposal

Write a proposal a reviewer can trace from each promised behavior through its contracts, boundaries, rollout, and controls, using `$spellbinding-sentences` for the prose.

1. **Decision:** state the decision asked for, the mechanism, the invariants that must not change, and the main tradeoff.
2. **Boundaries:** give each API, file format, package name, URL, or credential an owner and a compatibility choice (preserve, versioned migration, or breaking release).
3. **Path:** trace caller input through validation, storage or deployment, and runtime, naming the data shape and failure behavior at each handoff.
4. **Privilege:** give each privileged action a named principal, least-privilege credential, input validation, and an approval point before anything becomes visible.
5. **Rollout:** stage from a manual observable proof to guarded automation, with verification, rollback, and the condition for removing the old path.
6. **Review:** pair each risk with a control, and keep only open questions that change the design, each with an owner.

Open with **Proposal**, **Executive summary**, **Goals**, and **Non-goals**, add whatever sections the decision needs, and close with **References**.

Done when every goal and contract has a mechanism, every risk has a control, and every open question has an owner.
