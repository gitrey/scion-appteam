---
name: groom
description: Perform backlog grooming in JIRA
---

# /groom — Perform backlog grooming in JIRA

## Trigger

User invokes `/groom` to groom the active product backlog.

## Instructions

1. **Retrieve Ungroomed Issues** — Invoke the native Atlassian MCP tool `search_issues` with JQL:
   `project = "${JIRA_PROJECT_KEY:-APPT}" AND status = Backlog ORDER BY created`
2. **Audit Descriptions & Criteria** — For each issue in the backlog:
   - Verify it has a clear User Story (_As a..._).
   - Ensure it contains testable, concrete **Acceptance Criteria**.
   - If details are missing or ambiguous, use `add_comment` or `update_issue` to clarify.
3. **Refine Priorities** — Check for dependencies between issues. Re-prioritize issues to ensure blockers or prerequisites are handled first by invoking `update_issue` with parameters:
   - `issueIdOrKey`: "<issue-id>"
   - `priority`: "<priority>"
4. **Verify local sync** — Compare with the local `docs/BACKLOG.md`. If new
   items were added to JIRA, coordinate with the TPM to ensure the local mapping
   is accurate.
5. **Grooming Summary** — Present a summary of all tickets reviewed, updated, or
   created during the grooming session, and note any blockers that require
   PO/User attention.

## Project Context

- **Project:** appteam
