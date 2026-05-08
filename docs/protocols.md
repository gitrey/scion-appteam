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

## Messaging & Hub
- **Hub Usage:** Use the Hub for all inter-agent communication via `scion message`.
- **Permissions:** If you encounter 403 errors, report them to the PO/TPM immediately for permission auditing.
