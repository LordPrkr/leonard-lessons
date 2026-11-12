---
name: code-brain-distill
disable-model-invocation: true
description: "Distill plan and review artifacts into discoverable repo-wide Code Brain documentation."
---

# Code Brain Distill

## 1. Extract

Read the supplied artifacts (default: `plans/**` and `review/*.md`) and keep only current, evidence-backed findings reusable beyond their original task.

Done when each candidate is verified against `HEAD` and absent from existing docs.

## 2. Promote

Update the owning document in place—`domain/` for terms and decisions, `resources/` for agent preferences, otherwise the matching Diátaxis folder under `docs/`—and link the source artifact as provenance. Ask before replacing contradicted docs, and keep `docs/README.md` routing to every canonical document.

Done when every promoted claim has exactly one home reachable from `docs/README.md`.

## 3. Report

List promoted, updated, and skipped candidates with reasons.

Done when the user can audit each decision without rereading the sources.
