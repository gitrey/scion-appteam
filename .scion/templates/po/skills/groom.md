---
name: groom
description: Perform backlog grooming in JIRA
---

# /groom — Perform backlog grooming in JIRA

## Trigger

User invokes `/groom` to groom the active product backlog.

## Instructions

1. **Retrieve Ungroomed Issues** — Pull all unprioritized or incomplete issues
   from JIRA:
   ```bash
   jira issue list --status "Backlog" --order-by "created"
   ```
2. **Audit Descriptions & Criteria** — For each issue in the backlog:
   - Verify it has a clear User Story (_As a..._).
   - Ensure it contains testable, concrete **Acceptance Criteria**.
   - If details are missing or ambiguous, add detailed comments or updates to
     clarify.
3. **Refine Priorities** — Check for dependencies between issues. Re-prioritize
   issues to ensure blockers or prerequisites are handled first:
   ```bash
   jira issue edit <issue-id> --priority "<priority>"
   ```
4. **Verify local sync** — Compare with the local `docs/BACKLOG.md`. If new
   items were added to JIRA, coordinate with the TPM to ensure the local mapping
   is accurate.
5. **Grooming Summary** — Present a summary of all tickets reviewed, updated, or
   created during the grooming session, and note any blockers that require
   PO/User attention.

## Project Context

- **Project:** appteam
