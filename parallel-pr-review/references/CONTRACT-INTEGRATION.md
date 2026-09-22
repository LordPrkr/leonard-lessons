# Contract integration

- **Boundary preservation:** Trace every changed method or RPC parameter through each adapter, provider, serializer, mock, and caller. Check omitted versus `undefined` versus `null`, added optional arguments such as `AbortSignal`, and default values at the actual runtime boundary.
- **Parity:** When web, extension, background, legacy, new, or equivalent endpoints implement the same policy, compare their observable behavior. Flag intentional divergence only when the diff lacks an explicit reason.

**Complete when:** every changed contract has a traced boundary path and every relevant equivalent implementation has a demonstrated parity decision.