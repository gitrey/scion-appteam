---
name: pipeline
description: Spin up the full agent team
---

# /pipeline — Spin up the full agent team

## Trigger

User invokes `/pipeline` with a feature description or milestone name.

## Instructions

1. **Create a team** — Use `TeamCreate` with a descriptive team name based on the feature (e.g., `feature-dark-mode`)
2. **Create tasks** — Use `TaskCreate` to create work items for the pipeline:
   - **Task 1:** PM — Define requirements and create spec in `docs/specs/`
   - **Task 2:** db — Design relational DDL schemas and generate seed datasets
   - **Task 3:** TPM — Create backlog items and coordinate SWE assignments
   - **Task 4+:** SWE — Implement the feature (one task per work item)
   - **Task N:** SWE-Test — Run tests and verify acceptance criteria
   - **Task N+1:** ui-test — Run UI regression and visual tests
   - **Task N+2:** perf-test — Execute Locust load tests and profile latencies
   - **Task N+3:** secops — Perform security audits and SCA vulnerability scans
   - **Task N+4:** devops — Build containers, provision infra, and deploy to GCP
   - **Task N+5:** doc — Synchronize OpenAPI schemas and system wikis
   - **Task N+6:** sre — Probe deployment health and provision alerting policies
   - **Task N+7:** Reviewer — Code review (if reviewer agent exists)
3. **Spawn agents** — Use the `Agent` tool with `team_name` parameter to launch each agent in its own tmux pane. Always use model `gemini-3.1-flash-lite-preview` for all agents:
   - PM agent (reads `.gemini/agents/pm.md`)
   - db agent (reads `.gemini/agents/db.md`)
   - TPM agent (reads `.gemini/agents/tpm.md`)
   - SWE-1 agent (reads `.gemini/agents/swe-1.md`)
   - SWE-2 agent (reads `.gemini/agents/swe-2.md`)
   - SWE-Test agent (reads `.gemini/agents/swe-test.md`)
   - ui-test agent (reads `.gemini/agents/ui-test.md`)
   - perf-test agent (reads `.gemini/agents/perf-test.md`)
   - secops agent (reads `.gemini/agents/secops.md`)
   - devops agent (reads `.gemini/agents/devops.md`)
   - doc agent (reads `.gemini/agents/doc.md`)
   - sre agent (reads `.gemini/agents/sre.md`)
4. **Assign tasks** — Use `TaskUpdate` with `owner` set to each agent's name
5. **Follow the mandatory pipeline:**
   - PO feedback → PM creates spec → db designs relational schema & seed → TPM creates backlog ➔ SWEs implement ➔ QA Triad verifies (SWE-Test code, ui-test visual, perf-test load, secops security) ➔ Reviewer reviews & doc updates api ➔ devops deploys to GCP ➔ sre probes health & alerts
   - docs/BACKLOG.md, docs/PROGRESS.md, and docs/RELEASENOTES.md MUST be updated
6. **Monitor and coordinate** — Use `SendMessage` to communicate with agents and track progress
7. **Shutdown gracefully** — Send `shutdown_request` to each agent when all work is complete
8. **Clean up** — Use `TeamDelete` after all agents have shut down

## Project Context

- **Project:** appteam
- **Owner:** Scion Agent
- **Model:** `gemini-3.1-flash-lite-preview`
- **Agent definitions:** `.gemini/agents/`
- **Pipeline diagram:** `docs/PIPELINE.md`
