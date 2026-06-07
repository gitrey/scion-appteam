# Team Protocols

## Git Configuration
- **Non-interactive Mode:** All agents must use non-interactive git commands to prevent stalling.
- **Environment Variables:**
  - `GIT_TERMINAL_PROMPT=0`
  - `PAGER=cat`
- **Commands:**
  - Prefer `git commit -m "..."` over `git commit`.
  - Use `git merge --no-edit` or `git merge -m "..."`.
  - Use `git push --no-verify` if hooks cause interactive delays.

## Synchronization
- **Fetch/Pull:** Always execute `git fetch` or `git pull` before reading `docs/BACKLOG.md` or `docs/specs/` to ensure you have the latest state.
- **Commit/Push:** Push changes immediately after updating tracking files to minimize merge conflicts.
- **Feature Branches:** Before starting any new feature branch, ensure you are on `main` and pull/sync the latest remote changes (`git checkout main && git pull`), then create the new feature branch from `main`. Never create a feature branch off of another feature branch.

## JIRA Integration Fallback
- **Environment Check:** Check for these environment variables before trying to use JIRA: `ATLASSIAN_API_TOKEN`, `ATLASSIAN_AUTH_TOKEN`, `ATLASSIAN_USER_EMAIL`, `JIRA_CLOUD_ID`, `JIRA_PROJECT_KEY`.
- **Fallback Behavior:** If JIRA is not configured, agents must skip all JIRA-related tool calls, commands, and transitions. Rely entirely on the local tracking files (such as `docs/BACKLOG.md`), logging/reporting that JIRA integration has been bypassed.

## Messaging & Hub
- **Hub Usage:** Use the Hub for all inter-agent communication via `scion message`.
- **Permissions:** If you encounter 403 errors, report them to the PO/TPM immediately for permission auditing.
