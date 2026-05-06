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
5. **Create the JIRA Ticket** — Use JIRA CLI or API:
   ```bash
   jira issue create --type "<type>" --summary "<title>" --description "<description_and_criteria>" --priority "<priority>"
   ```
6. **Sync with Local Backlog** — Inform the TPM to add the ticket link and
   reference to the local `docs/BACKLOG.md` for cross-referencing.
7. **Confirm Status** — Report the newly created JIRA ticket ID, title, and
   priority back to the user.

## Project Context

- **Project:** appteam
