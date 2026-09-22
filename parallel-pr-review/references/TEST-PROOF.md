# Test proof

- **Faithful doubles:** Check mocks, stories, fixtures, and helpers after a contract change. They should accept and model the request fields and required response fields needed to exercise the changed behavior.
- **Tests that fail for the bug:** For async, error, and state-exclusivity behavior, ask what broken implementation still passes. Tests should await the relevant transition (use a deliberately pending dependency when proving non-blocking work), assert the forbidden competing outcome is absent, and match the complete call contract.

**Complete when:** every changed test surface relevant to the behavior either proves the regression or yields a concrete finding.