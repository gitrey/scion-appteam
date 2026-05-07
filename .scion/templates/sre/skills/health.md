---
name: health
description: Verify deployed microservice health and provision Alerting Policies in GCP
---

# /health — Verify Microservice Health and Provision Alerting Policies

## Trigger

User invokes `/health` with a target service host and specification ID (e.g., `/health "https://checkout.appteam.net" "F-0031"`).

## Instructions

1. **Execute Uptime Probes** — Perform HTTP liveness and readiness checks on `/healthz` and `/readyz`:
   ```bash
   curl -sf -o /dev/null -w "%{http_code}" <service-host>/healthz
   # and
   curl -sf -o /dev/null -w "%{http_code}" <service-host>/readyz
   ```
2. **Verify Response Payloads** — Validate that response payloads contain compliant JSON structures (e.g., `{"status": "UP"}`) and HTTP response status code is `200`.
3. **Provision Observability Infrastructure (Terraform)** — Navigate to `terraform/monitoring/` and provision Cloud Monitoring Uptime Checks and Alerting Policies:
   ```bash
   terraform init
   terraform apply -auto-approve
   ```
4. **Groom & Commit Monitoring Assets** — Stage and commit the updated alerting policies:
   ```bash
   git -c user.name="Andrey Shakirov" -c user.email="andreyshakirov@google.com" add terraform/monitoring/
   git -c user.name="Andrey Shakirov" -c user.email="andreyshakirov@google.com" commit -m "sre: add Uptime Checks and Alerting Policies for <spec-id>"
   ```
5. **Reliability Summary** — Present a concise post-deployment health report:
   - Active liveness/readiness probe status (UP/DOWN).
   - Provisioned Alerting Policies and Notification Channels.
   - Recommended CPU/memory limits or latency warnings based on initial probes.

## Project Context

- **Project:** appteam
