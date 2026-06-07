---
name: groom
description: Perform backlog grooming in JIRA
---

# /groom — Perform backlog grooming in JIRA

## Trigger

User invokes `/groom` to groom the active product backlog.

## Instructions

1. **Verify JIRA Configuration** — First check for these environment variables before trying to use JIRA: `ATLASSIAN_API_TOKEN`, `ATLASSIAN_AUTH_TOKEN`, `ATLASSIAN_USER_EMAIL`, `JIRA_CLOUD_ID`, `JIRA_PROJECT_KEY`. If they are not configured, abort JIRA operations, log that JIRA integration is skipped due to missing environment variables, and rely solely on the local `docs/BACKLOG.md` file.
2. **Retrieve Ungroomed Issues** — If JIRA is configured, invoke the native Atlassian MCP tool `search_issues` with JQL:
   `project = "${JIRA_PROJECT_KEY:-APPT}" AND status = Backlog ORDER BY created`
3. **Audit Descriptions & Criteria** — For each issue in the backlog:
   - Verify it has a clear User Story (_As a..._).
   - Ensure it contains testable, concrete **Acceptance Criteria**.
   - If details are missing or ambiguous, use `add_comment` or `update_issue` to clarify.
4. **Refine Priorities** — Check for dependencies between issues. Re-prioritize issues to ensure blockers or prerequisites are handled first by invoking `update_issue` with parameters:
   - `issueIdOrKey`: "<issue-id>"
   - `priority`: "<priority>"
5. **Verify local sync** — Compare with the local `docs/BACKLOG.md`. If new
   items were added to JIRA, coordinate with the TPM to ensure the local mapping
   is accurate.
6. **Grooming Summary** — Present a summary of all tickets reviewed, updated, or
   created during the grooming session, and note any blockers that require
   PO/User attention.

## Project Context

- **Project:** appteam
