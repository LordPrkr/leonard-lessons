---
name: draft-message
description: "Draft a technical message, revise it with your feedback, and copy the approved version to your clipboard."
disable-model-invocation: true
---

# Draft Message

Prepare a message for the user to send. Sending or posting is outside this workflow.

## 1. Draft

Invoke [/spellbinding-sentences](../spellbinding-sentences/SKILL.md) and apply its writing workflow to the message.

Use the supplied draft, facts, and conversation context to identify the recipient, what they already know, and the intended outcome. Ask a focused question if missing information would materially change the message; otherwise draft immediately. Match the user's requested tone, length, and channel, using a concise collegial tone by default.

Present one complete, ready-to-send message, with any questions or commentary outside it. Ask for feedback or approval.

Done when the proposed message satisfies the writing workflow and the user can review it as a standalone message to the recipient.

## 2. Revise until approved

Wait for the user's response. Incorporate feedback into the latest draft, reapply `/spellbinding-sentences`, and present the complete revised message. Preserve accepted wording and substance outside the requested changes. Repeat this step after each revision.

Approval must explicitly accept the latest displayed version, such as “approved,” “looks good,” or “copy it.” A response that also requests edits is feedback: show the edited version and wait for fresh approval. If approval is ambiguous, ask whether to copy the current version. If the user cancels, stop.

Done when the user explicitly approves the latest displayed message without requesting further changes.

## 3. Copy

Read [clipboard guidance](clipboard.md) and copy only the exact approved message, preserving its line breaks and intended formatting. Exclude review labels, enclosing display fences, approval prompts, and assistant commentary. Approval freezes the text; further edits return to step 2.

Done when clipboard success is confirmed and briefly reported, or copying is unavailable or fails and the approved message is provided for manual copying with an honest explanation.
