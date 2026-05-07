---
name: logs
description:
  Query application logs from Google Cloud Run or GKE for troubleshooting
---

# /logs — Query Application Logs for Troubleshooting

## Trigger

User invokes `/logs` with a service name, pod name, or epic identifier to
retrieve active logs (e.g., `/logs "appteam-checkout" --limit 50`).

## Instructions

1. **Detect Platform Context** — Identify if the target service is deployed on
   **Google Cloud Run** or **Kubernetes (GKE)** by inspecting active
   configurations or querying:
   ```bash
   gcloud run services list --quiet
   # and
   kubectl config current-context
   ```
2. **Query Google Cloud Run Logs** — If the target is a Cloud Run service,
   retrieve the logs non-interactively using `gcloud`:
   ```bash
   gcloud beta run services logs read <service-name> --limit 100 --region us-central1 --quiet
   ```
   Alternatively, query Cloud Logging directly for custom formatting:
   ```bash
   gcloud logging read "resource.type=\"cloud_run_revision\" AND resource.labels.service_name=\"<service-name>\" severity>=WARNING" --limit 50 --format="table(timestamp,severity,textPayload)" --quiet
   ```
3. **Query Kubernetes (GKE) Logs** — If the target is on GKE, locate the active
   pod and stream logs:

   ```bash
   # 1. Get the exact pod name using labels
   kubectl get pods -l app=<service-name> -o jsonpath="{.items[0].metadata.name}"

   # 2. Stream the last 100 lines of logs with timestamps
   kubectl logs <pod-name> --tail=100 --timestamps
   ```

4. **Audit Logs for Critical Errors** — Parse the retrieved log lines for error
   indicators:
   - Keywords: `ERROR`, `Exception`, `FATAL`, `CRITICAL`, `5xx`, `Timeout`,
     `Connection Refused`.
   - Capture the full stack trace or error context where found.
5. **Log Troubleshooting Report** — Output a structured report back to the team:
   - Active service state and deployment platform.
   - A clean table or block containing the recent log extract.
   - Highlighted error stack traces and recommended troubleshooting steps for
     the SWEs.

## Project Context

- **Project:** appteam
