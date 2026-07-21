---
name: jira-ticket
description: Create Jira tickets from a repository change or problem statement. Use when the user wants a Jira issue created without preparing a GitHub pull request.
---

# Jira Ticket

Apply `/spellbinding-sentences` to the summary and description.

## 1. Establish intent

Gather the problem, motivation, expected outcome, Jira project, and issue type from the request and relevant repository context. Prefer a user-supplied project or repository convention. Ask one focused question if the project or motivation remains ambiguous.

Search Jira and the branch name for an existing issue before creating one. If the requested work already has an issue, return it instead of creating a duplicate.

**Complete when:** the ticket's project, type, summary, problem, and expected outcome are known, and no existing issue covers the work.

## 2. Draft the ticket

Write a concise summary and a description centered on background, user or operational impact, and the intended outcome. Do not narrate implementation details that belong in a pull request.

Unless the user says otherwise, create a Task assigned to Parker in the active sprint and move it to In Progress. If any default is unavailable, preserve the created ticket and report the unmet field rather than guessing.

**Complete when:** the draft explains why the work matters and every requested or default field has a concrete value.

## 3. Create and verify

Create the issue with the available Jira integration, then read it back. Return its key and URL.

**Complete when:** Jira contains exactly one new issue with the approved content, or an existing matching issue has been returned without mutation.
