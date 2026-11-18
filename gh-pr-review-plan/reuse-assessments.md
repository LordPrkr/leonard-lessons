# Reuse prior assessments

Recollect current feedback on every run. New replies, edits, deletions, and resolution changes can occur at the same PR head.

At collection, record a fingerprint for each group's supporting feedback and relevant GitHub state. Include source IDs and URLs, authors, bodies, and each relevant thread's full set of comments, file and line anchors, and resolved and outdated flags. Use a deterministic hash of the fields in stable ID and field order. Save the fingerprint beside the completed assessment and carry it into the final plan. Update the saved assessment and its fingerprint together after verification.

Reuse a completed assessment only when the PR, base, head, merge base, source membership, and fingerprint match, and no new feedback elsewhere affects its evidence or conclusion. Reassess groups with missing fingerprints, changed context, or incomplete evidence. Remove prior groups absent from the current inventory when writing the final plan.

Done when every reused assessment matches current evidence and every other current group is queued for assessment.
