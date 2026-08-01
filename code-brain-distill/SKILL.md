---
name: code-brain-distill
disable-model-invocation: true
description: "Distill plan, review, and dream artifacts into discoverable repo-wide Code Brain documentation."
---

# Code Brain Distill

Turn activity-scoped evidence into canonical project documentation. Follow `/code-brain` for repository identity, evidence, and documentation ownership. Source artifacts remain unchanged provenance; `docs/` holds the maintained result.

## 1. Select sources

Use explicit artifact paths when supplied. Otherwise scan `plans/**/notes.md`, `notes/plans/*.md`, `review/*.md`, and `notes/dreams/*.md`. Read existing `docs/`, relevant `domain/` context and ADRs, and `resources/` before extracting candidates.

Done when every selected artifact and existing canonical destination that could already own its lessons is known.

## 2. Extract candidates

Retain only evidence-backed findings reusable beyond the originating task: repository conventions, stable architecture or behavior, recurring procedures, operational hazards, and explanations of constraints or tradeoffs. Reject task status, one-off implementation detail, transient failures, guesses, and claims whose repository evidence no longer matches `HEAD`.

Deduplicate by normalized claim and applicability boundary. Treat `Documentation candidates`, review `Lessons`, and high-confidence dream memories as strong leads, not automatic truth.

Done when every retained candidate is current, reusable, evidence-backed, and absent from or materially improves canonical memory.

## 3. Choose the canonical destination

Keep domain terms and qualifying decisions under `domain/`, agent workflow preferences under `resources/`, and route remaining project documentation with the Diátaxis compass:

- action + learning → tutorial
- action + work → how-to
- knowledge + work → reference
- knowledge + understanding → explanation

Prefer the reader's topic and repository vocabulary over mirroring source artifact names. Update an existing topic document when it already owns the subject.

Done when each candidate has exactly one destination or an explicit skip reason.

## 4. Promote

Write or update the canonical document in place. Preserve useful existing content, remove duplication, apply `/code-brain` evidence, and link the source artifact as provenance. Ask before replacing contradicted canonical memory. When at least one canonical `docs/` document exists after promotion, create or update `docs/README.md` with short, reader-oriented links grouped by the categories that actually exist. When `AGENTS.md` exists, keep one Canonical memory link to that landing page; never create missing spine files as a side effect.

Done when every promoted claim has one source of truth, current material evidence, source provenance, and—when canonical docs exist—a route from `docs/README.md`.

## 5. Report

Report selected artifacts, promoted documents, updated documents, skipped candidates with reasons, stale or contradictory claims, and missing spine links.

Done when the user can audit every promotion and skip without rereading all source artifacts.
