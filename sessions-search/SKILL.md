---
name: sessions-search
description: "Search local Pi session transcripts for a topic, prior decision, implementation detail, or command outcome."
---

# Sessions Search

Find the relevant evidence in local Pi sessions, then report it concisely.

## Steps

### 1. Set the search

Extract the user's topic. When it is ambiguous, ask for the term, project, approximate date, or outcome sought.

Search `~/.pi/agent/sessions` by default. If it does not exist, report that and ask for the configured session directory; respect a user-supplied directory.

Done when the topic and session root are unambiguous.

### 2. Search transcripts

Search `*.jsonl` recursively with a case-insensitive fixed-string query first. Refine with the user's project, date, or additional distinctive terms when the initial results are broad. Use context around matches and inspect the matching session records enough to distinguish user requests, agent conclusions, and tool evidence.

Done when every reported session has a relevant, inspected match rather than a filename-only hit.

### 3. Report evidence

Return the strongest matches, ordered by relevance. For each, give:

- session path
- project or working directory and date when present in its session record
- a short relevant excerpt or summary
- what the session establishes, with uncertainty called out

Keep excerpts minimal and redact credentials, tokens, personal data, and unrelated command output. State when no matching session is found and name the search terms and root used.

Done when the user can reopen the relevant transcript or proceed from the stated evidence.
