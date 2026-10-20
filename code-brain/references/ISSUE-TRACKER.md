# Set Up the Project's Issue Tracker

Use this branch when the user supplies or changes issue-tracker information, or a workflow needs missing or incomplete tracker configuration. Its output is `$CODE_BRAIN_ROOT/<repo>/ISSUE_TRACKER.md`, resolved through the repository identity rules in `$code-brain`.

## 1. Identify the tracker

Read existing `ISSUE_TRACKER.md`, repository instructions, remotes, and relevant tracker configuration. Start with the tracker and project the user names. If none is named, propose the tracker supported by project evidence and ask the user to identify it when evidence is inconclusive.

Done when the tracker and exact repository, project, or team scope are identified, with an access method available for inspection or an explicit access gap.

## 2. Inspect precedent

Inspect representative open and completed issues in that scope, their histories, and any linked workflow guidance. Look for how people actually find and create work, structure issues, claim ownership, record dependencies, change status, and close or cancel work. Distinguish observed conventions from proposed changes; a remote URL alone does not establish a workflow.

When access is unavailable or precedent is absent or inconsistent, report the gap and ask the user for the missing workflow details. Keep unverified claims explicit rather than substituting a default workflow.

Done when the proposed workflow is grounded in cited tracker examples and guidance, with every evidence gap identified for confirmation.

## 3. Confirm the workflow

Show the proposed `ISSUE_TRACKER.md` contents: tracker location and scope, available tools or commands, issue conventions, ownership and status transitions, dependency handling, and links between issues and Code Brain context. Cite the examples supporting the proposal and identify choices supplied by the user. Ask the user to confirm or correct this concrete workflow before writing it to Code Brain. If corrections change the tracker or scope, inspect precedent there before presenting the revised draft.

This setup records the project's existing workflow and agreed changes. It does not define triage labels, change tracker settings, or set up domain documentation.

Done when the user explicitly confirms the complete proposed workflow and any unresolved evidence gaps are recorded as such in the draft.

## 4. Persist the configuration

Write the confirmed contents to `ISSUE_TRACKER.md`, updating an existing file in place while preserving unrelated user content. Keep this file focused on configuration and workflow; issues remain in the selected tracker. Use the [project-spine template](./PROJECT_SPINE.md) for its shape. Add or repair the relative link from the project's `AGENTS.md`, and report every newly created artifact's resolved absolute path under `$code-brain`'s creation contract.

Done when the saved configuration matches the confirmed draft, the router link resolves, and the user has the configuration's absolute path.
