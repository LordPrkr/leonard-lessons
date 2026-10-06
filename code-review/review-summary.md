# Review summary

## Manual review priorities

Use these categories to direct the user's manual review. Cover the backend categories for backend changes, frontend categories for frontend changes, and both for a mixed change. Classify by the behavior affected rather than directory names. Keep Standards and Spec findings complete; these priorities govern the manual review guide.

| Scope | Category | Inspect |
| --- | --- | --- |
| Backend | API contract changes | Added, removed, or changed endpoints; request and response fields or types; status codes, errors, authentication, and compatibility with existing clients. |
| Backend | Database query changes | Changed SQL or ORM reads and writes, including filters, joins, ordering, pagination, transaction boundaries, affected rows, and query cost under the expected workload. |
| Backend | Database schema changes | Migrations and changes to tables, columns, types, indexes, or constraints; backfills, existing data, deployment order, locking, and rollback. |
| Frontend | Package contract changes | Added, removed, or changed public exports, types, signatures, and package entry points; affected consumers and compatibility. |
| Frontend | New network requests | Requests introduced directly or through clients, hooks, or SDKs, including new calls to existing endpoints. Inspect the destination, method, payload, credentials, triggering conditions, frequency, retries, and server effects. |

Order manual review areas by the concrete consequence and difficulty of reversing the change: persisted data changes, deployed consumer dependencies, and external effects can survive a code revert. Explain the actual consequence and recovery requirement supported by the source. Label operational assumptions and missing evidence explicitly.

## Final response

1. **Explain what the PR accomplishes.** Open with the resulting behavior, who or what benefits, and the implementation path that makes it possible. For a local review, describe the compared changes. Ground the overview in the reviewed source and distinguish implemented behavior from the spec's intent.

   **Complete when:** the reader can explain what changes and how the code produces that result without reading the findings first.

2. **Direct manual review.** For each changed priority area, name its category and link to the relevant file and lines at the pinned revision. Explain the previous and new behavior, the affected consumers or data, and whether reversal requires more than reverting code. Give the user a concrete check or decision, such as verifying that an existing client accepts a response or that a migration preserves existing rows. Include the available test or validation evidence and its limits where they affect that decision.

   Include a short, language-tagged code or diff excerpt from the reviewed source for each area, retaining enough surrounding code to make the behavior clear. Show before and after when needed to expose the contract or query change; removed code comes from the pinned base. Use actual source rather than invented examples or proposed fixes, and identify omissions. Group related hunks around one review decision, with links to supporting locations.

   State which applicable categories have no changes in one compact sentence. When inspection is incomplete, name the unverified category and missing evidence. If no priority areas changed, say so explicitly. A change can warrant manual review even when the agent found no defect.

   **Complete when:** every changed priority area has a source link, an accurate excerpt, a consequence, and a concrete manual check; every remaining applicable category is marked unchanged or unverified.

3. **Report the agent's findings and delivery.** Follow the guide with the separate Standards and Spec reports prepared during aggregation. End with each axis's finding count and worst issue, or its skip or failure. For GitHub PRs, include the pending review link and saved finding count, or explain why posting was skipped or failed and include unsaved findings. State that staged comments remain pending for the user to submit.

   **Complete when:** the reader can distinguish manual review priorities from detected defects, assess both review axes separately, and locate any pending comments or understand the delivery failure.
