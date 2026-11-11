# Handoff Routing

The session that performed wayfinding selects one route before invoking `$handoff`. These selection rules guide document preparation; the receiving session gets the selected instructions, not this decision tree.

## Select the entry skill

- **Slicing:** choose `$code-brain-slicing` when a scoped tracker project still needs setup or delivery stories still need definition or confirmation.
- **Planning:** choose `$code-brain-planning` when a bounded first slice is already agreed and no project or backlog setup remains. Supply the existing story and project references when present, or the agreed slice scope directly.

## Write the selected route

Create one `Instructions for the next session` section using exactly one entry block below. Replace placeholders with inspected references and the concrete scope. Omit the unused entry block and the selection rules from the generated document. Order suggested skills to match the selected entry and its continuation.

### Slicing entry

```md
## Instructions for the next session

Invoke `$code-brain-slicing` for <effort and source references> to define and confirm the scoped tracker project and delivery stories. After publication, follow slicing's prompt asking whether the user is ready to dispatch. On confirmation, invoke `$code-brain-dispatch` with the published index and project so each ready slice begins implementation planning in its own T3 Code thread. If dispatch is deferred, stop with the published references.
```

### Planning entry

```md
## Instructions for the next session

Invoke `$code-brain-planning` for <named first slice and its concrete references> to create its implementation plan.
```

### Planning continuation

Append this only to the planning entry block; the slicing route follows its dispatch decision instead:

```md
Follow the planning workflow's review and explicit user approval steps, then implement and verify the approved slice through the same workflow. Leave later slices for subsequent work.
```

When a wayfinding map exists, also append a direct instruction naming its actual path: link that map from each resulting plan's Precedent and link the plan from the map's Outcome. For the slicing route, carry this instruction into dispatched handoffs. Without a map, omit that instruction.
