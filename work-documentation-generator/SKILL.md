---
name: work-documentation-generator
description: Prepare linked Jira and GitHub work documentation. Use when a branch ready for review needs a Jira ticket, a pull-request description, and reciprocal links between them.
---

# Work Documentation Generator

Coordinate `/jira-ticket` and `/github-pr-description`; keep their artifact rules in those skills.

## 1. Resolve the Jira issue

Use an issue supplied by the user or referenced by the branch or existing pull request. If none exists, invoke `/jira-ticket` with the branch's problem and repository context.

**Complete when:** one Jira issue key and URL are known.

## 2. Prepare the pull request

Invoke `/github-pr-description` with the Jira URL and require the issue link at the top of the body.

**Complete when:** the current branch has one open pull request whose finished body links the Jira issue.

## 3. Link Jira back to GitHub

Read the Jira comments. If none links the pull request, add one concise comment with its URL; do not add a duplicate.

**Complete when:** the Jira issue links the pull request and the pull-request body links the Jira issue.

## Result

Return the Jira and pull-request URLs and state whether each artifact was created or updated.
