---
name: technical-design-proposal
description: "Design proposal workflow for changes that cross API, runtime, security, compatibility, release, or operational boundaries. Use when proposing a system design, SDK capability, migration, integration, or deployment path."
---

# Technical Design Proposal

Turn an ambiguous change into an executable decision. A proposal is complete when a reviewer can trace each promised behavior through its contracts, boundaries, rollout, and controls.

## Steps

### 1. Establish the decision

Identify the reader, decision owner, current behavior, proposed behavior, and decision that the document asks them to make. Name the invariants: the source of truth, behavior, ownership, or capability that must remain unchanged. State the mechanism in the opening Proposal paragraph: name the systems, direction of data or authority, and the resulting boundary.

Use `/spellbinding-sentences` to draft or revise every explanatory section.

Done when the Proposal and Executive summary state what changes, the invariants, why the change is needed, and its primary cost or tradeoff.

### 2. Draw the boundary

Write explicit goals and non-goals. Identify the source of truth, every trust boundary, the owner of each API or persisted contract, and which compatibility surfaces need an intentional decision.

Treat a serialized value, package name, CLI command, file format, URL, generated API, artifact, and credential as a contract until its owner says otherwise. For each changed contract, choose preservation, a versioned migration, or a deliberately breaking release.

Done when every system boundary and externally observable change has an owner and a compatibility decision.

### 3. Specify the path

Describe the smallest supported path from author or caller input through build, validation, storage or deployment, and runtime behavior. Use a concrete API or workflow example when behavior flows through a system; use an exhaustive change inventory when the decision is a migration or rename. Explain how the implementation produces the behavior.

At each applicable handoff, specify identity, data shape, validation, and failure behavior. For asynchronous or repeated work, specify ordering, idempotency, concurrency, and how operators observe the outcome.

Done when an implementer can name every applicable handoff or changed surface, its input and output or before-and-after state, its validator, and what happens when it fails.

### 4. Account for privilege

Map each principal, credential, execution environment, and externally controlled input. State the minimum permission, when credentials become available, and the check that prevents an input from crossing a broader boundary than intended.

For browser or service bridges, specify trusted identities and origins, protocol version and message shape, correlation or revision rules, and the exact capability exposed. For publish, import, or disclosure paths, treat a dry run that creates visible state as a disclosure event and give it the same approval boundary as a live run.

Done when every privileged action has a named principal, a least-privilege credential path, input validation, and an approval or review point before disclosure.

### 5. Make the transition reversible

When the change has a rollout, describe the ordinary developer or operator cycle, then stage rollout from a manual, observable proof through guarded automation. Include prerequisites owned by other teams, the first production-like execution, verification, rollback, and the condition for removing the old path.

Keep public release, adoption, and destructive cutovers explicit unless the proposal establishes the automation and its control boundary.

Done when a maintainer can execute the applicable rollout in order, prove each stage worked, recover from failure, and know when the predecessor may be removed.

### 6. Close the review

List risks as concrete failure modes paired with preventive or detective controls. Keep unresolved questions only when their answer changes scope, design, ownership, or rollout; name the decision owner and the blocking effect.

Check every goal, non-goal, contract, boundary, operational path, and rollout stage against the proposed implementation. Remove background that does not change a decision.

Done when every material risk has a control, every open question has an owner and consequence, and no promised behavior lacks a corresponding mechanism.

## Required structure

Every design document has these sections:

1. **Proposal** — the decision, mechanism, preserved behavior, and primary tradeoff.
2. **Executive summary** — the current state, proposed change, preserved behavior, and cost in a short standalone overview.
3. **Goals** — the outcomes the design must deliver.
4. **Non-goals** — nearby work or capability the design intentionally leaves out, with the boundary when needed.

These required sections are the document's opening spine, not its whole outline. Put project-specific sections after them when they make the decision reviewable. Choose those headings from the system and decision at hand; no fixed middle-section template applies. Close every document with **References**, linking the source documents, code, pull requests, and discussions that substantiate its claims.

Keep alternatives beside the constraint that rejects them. Use diagrams or tables only when they make a boundary, flow, or contract easier to verify than linear prose.
