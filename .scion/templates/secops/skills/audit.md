---
name: audit
description: Perform comprehensive security and dependency audits
---

# /audit — Perform Security and Dependency Audits

## Trigger

User invokes `/audit` with a specification ID to verify a feature's security (e.g., `/audit "F-0031"`).

## Instructions

1. **Audit Code Security (SAST)** — Scan the Go codebase for security vulnerabilities using `gosec` or `semgrep`:
   ```bash
   gosec -fmt=json -out=docs/security-reports/<spec-id>-gosec.json ./...
   ```
2. **Scan Dependencies (SCA)** — Audit external dependencies for known CVEs:
   ```bash
   govulncheck ./... > docs/security-reports/<spec-id>-vulncheck.txt
   ```
3. **Audit Plaintext Secrets** — Search changed files or git diffs for hardcoded keys, credentials, or API tokens. Ensure `.env` and private keys are listed in `.gitignore`.
4. **Groom & Commit Security Reports** — Stage and commit the generated vulnerability logs:
   ```bash
   git -c user.name="Andrey Shakirov" -c user.email="andreyshakirov@google.com" add docs/security-reports/
   git -c user.name="Andrey Shakirov" -c user.email="andreyshakirov@google.com" commit -m "sec: add security and vulnerability audit reports for <spec-id>"
   ```
5. **Deliver Security Summary** — Present a clear security audit report back to the team:
   - Total vulnerabilities found (categorized by Critical, High, Medium, Low).
   - Missing `.gitignore` entries or plaintext secrets discovered.
   - Relative markdown links to the saved security reports in `docs/security-reports/`.
   - Pass/Fail recommendation for PR review.

## Project Context

- **Project:** appteam
