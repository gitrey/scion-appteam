---
name: audit
description: Perform comprehensive security and dependency audits
---

# /audit — Perform Security and Dependency Audits

## Trigger

User invokes `/audit` with a specification ID to verify a feature's security (e.g., `/audit "F-0031"`).

## Instructions

1. **Detect Codebase Language & Stack** — Inspect the repository root for language identifiers:
   - `go.mod` -> **Go**
   - `requirements.txt` or `pyproject.toml` -> **Python**
   - `package.json` -> **Node.js**
2. **Audit Code Security (SAST)** — Scan the source code for security vulnerabilities using the appropriate non-interactive tool:
   - **Go:** Use `gosec` or `semgrep`:
     ```bash
     gosec -fmt=json -out=docs/security-reports/<spec-id>-gosec.json ./...
     ```
   - **Python:** Use `bandit` or `semgrep`:
     ```bash
     bandit -r . -f json -o docs/security-reports/<spec-id>-bandit.json
     ```
   - **Node.js / Polyglot:** Use `semgrep` (which supports Go, Python, Node, C#, etc.):
     ```bash
     semgrep scan --config=auto --json --output=docs/security-reports/<spec-id>-semgrep.json
     ```
3. **Scan Dependencies (SCA)** — Audit external dependencies for known CVEs based on the active stack:
   - **Go:** Use `govulncheck`:
     ```bash
     govulncheck ./... > docs/security-reports/<spec-id>-vulncheck.txt
     ```
   - **Python:** Use `pip-audit` or `safety`:
     ```bash
     pip-audit --format json --output docs/security-reports/<spec-id>-pipaudit.json
     ```
   - **Node.js:** Use `npm audit` or `yarn audit`:
     ```bash
     npm audit --json > docs/security-reports/<spec-id>-npmaudit.json
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
