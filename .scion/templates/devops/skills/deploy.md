---
name: deploy
description: Build and deploy microservices to Google Cloud Run
---

# /deploy — Build and Deploy Microservices to Google Cloud Run

## Trigger

User invokes `/deploy` with a target service name and optional image tag (e.g., `/deploy "appteam-checkout" "v1.1.0"`).

## Instructions

1. **Verify Prerequisites** — Check that local git status is clean and `gcloud` auth is configured.
2. **Run Local Build** — Ensure the application compiles and tests pass before building the container:
   ```bash
   go test ./... -v
   ```
3. **Build and Push Container Image** — Build the Docker container and push it to Google Artifact Registry (GAR) or Container Registry (GCR):
   ```bash
   docker build -t gcr.io/<project-id>/<service-name>:<tag> .
   docker push gcr.io/<project-id>/<service-name>:<tag>
   ```
4. **Provision Infrastructure (Terraform)** — If the deployment requires database, secrets, or network changes, navigate to the `terraform/` directory and apply changes:
   ```bash
   terraform init
   terraform apply -auto-approve
   ```
5. **Deploy to Cloud Run** — Execute the deployment non-interactively using the `--quiet` flag:
   ```bash
   gcloud run deploy <service-name> \
     --image gcr.io/<project-id>/<service-name>:<tag> \
     --platform managed \
     --region us-central1 \
     --quiet \
     --no-allow-unauthenticated
   ```
6. **Verify Service Health** — Perform an HTTP probe or curl on the returned service URL to verify successful startup and response.
7. **Report Back** — Provide a deployment summary including the service URL, Docker image tag, and Terraform resource updates.

## Project Context

- **Project:** appteam
