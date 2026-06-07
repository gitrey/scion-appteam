---
name: story
description: Create a structured JIRA Story or Bug
---

# /story — Create a structured JIRA Story or Bug

## Trigger

User invokes `/story` with a description of a new feature, task, or bug.

## Instructions

1. **Analyze the request** — Determine if the issue is a `Story` (new
   feature/value), `Bug` (unexpected behavior), or `Task` (engineering work).
2. **Draft the User Story** — Format as:
   > **As a** <user/persona>  
   > **I want to** <action/feature>  
   > **So that** <business value/benefit>
3. **Write Acceptance Criteria** — Use testable, clear Given-When-Then Gherkin
   formatting or a numbered checklist:
   - E.g., _Given the user is on the login page, when they input valid
     credentials, then they are redirected to the dashboard._
4. **Assign Priority** — Determine business priority (`High`, `Medium`, `Low`).
5. **Verify JIRA Configuration & Create Ticket** — Check for these environment variables before trying to use JIRA: `ATLASSIAN_API_TOKEN`, `ATLASSIAN_AUTH_TOKEN`, `ATLASSIAN_USER_EMAIL`, `JIRA_CLOUD_ID`, `JIRA_PROJECT_KEY`. If configured, invoke the native Atlassian MCP tool `create_issue` with parameters:
   - `projectKey`: Value of the `JIRA_PROJECT_KEY` environment variable (defaulting to "APPT")
   - `summary`: "<title>"
   - `description`: "<description_and_criteria>"
   - `issueType`: "<type>"
   - `priority`: "<priority>"
6. **Sync with Local Backlog** — If JIRA was used, inform the TPM to add the ticket link and reference to the local `docs/BACKLOG.md`. If JIRA is not configured, skip JIRA creation and work with the TPM to log the story directly into `docs/BACKLOG.md` as a local-only backlog item.
7. **Confirm Status** — Report the newly created status (including JIRA ticket ID, title, and priority if created, or a note indicating that JIRA was skipped and tracked locally) back to the user.

## Project Context

- **Project:** appteam
