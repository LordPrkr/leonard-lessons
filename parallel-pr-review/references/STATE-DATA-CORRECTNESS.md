# State and data correctness

- **State matrix:** Trace loading, success, empty, error, retry, cancellation, unmount/remount, account or tenant change, and gate-on/gate-off paths that the changed code can enter. Check that mutually exclusive UI states stay exclusive and stale state is cleared before it can render.
- **Race ownership:** For concurrent reads, mutations, retries, and subscriptions, identify which response may write shared state. Verify obsolete, failed, cancelled, or wrong-tenant responses cannot overwrite a newer authoritative result.
- **Cache lifetime:** Inspect cache keys for every result-shaping input and scope (user, tenant, environment, filters, force-refresh). Check invalidation, cancellation, cleanup, and `gcTime` against the intended lifetime; make sure a cache policy has one owner rather than accidental library defaults.
- **Pagination after filtering:** If one source supplies candidates and another filters them, follow an empty or short authorized page. Continuation must depend on whether the source is exhausted, not merely on rows surviving this page; check full final pages, next tokens, offsets, and requested page size.

**Complete when:** every relevant state, concurrency, cache, or traversal path has evidence of correct ownership or a concrete regression finding.