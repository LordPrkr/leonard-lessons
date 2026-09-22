# Operational assurance

- **Workflow trust path:** For CI, imports, releases, and credentials, trace who can trigger a write, read each secret, choose each ref, and bypass verification. Validate the intended artifact independently of its download and run the relevant verification when its configuration changes.
- **Runbook and telemetry consistency:** Compare changed automation to its runbook. For metrics, verify metric names, labels, cardinality bounds, lifecycle pairing, and test values match the tracker contract and preserve the distinction the dashboard needs.

**Complete when:** every changed operational boundary has a traced trust or telemetry path, or is inapplicable.