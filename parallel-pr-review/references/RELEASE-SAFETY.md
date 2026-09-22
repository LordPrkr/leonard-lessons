# Release safety

For a feature gate, required field, config default, or dependent PR, inspect each plausible merge order. A partially landed stack must preserve the safe legacy behavior; rollout gates and rate limits should fail closed.

**Complete when:** every relevant dependency or landing order has a traced safe behavior or a concrete regression finding.