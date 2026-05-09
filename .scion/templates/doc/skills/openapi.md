---
name: openapi
description: Generate and validate OpenAPI specs based on implemented API routes
---

# /openapi — Generate and Validate OpenAPI Specifications

## Trigger

User invokes `/openapi` with a specification ID to sync API documentation (e.g., `/openapi "F-0031"`).

## Instructions

1. **Audit Implemented Routes** — Scan the Go codebase for new REST or JSON-RPC endpoints, checking request payloads, query parameters, response schemas, and HTTP methods.
2. **Update OpenAPI Spec File** — Maintain and update the Swagger specification under `docs/api/openapi.yaml` by adding the new path parameters, models, and response codes.
3. **Generate Visual Sequence Diagrams** — Add or update an interactive Mermaid sequence map inside `docs/architecture/api-flow.md` to visualize the exact request/response flow of the new API.
4. **Groom & Commit API Docs** — Stage and commit the updated OpenAPI specifications:
   ```bash
   git -c user.name="Scion Agent" -c user.email="scion@users.noreply.github.com" add docs/api/docs/architecture/
   git -c user.name="Scion Agent" -c user.email="scion@users.noreply.github.com" commit -m "docs: update OpenAPI spec and sequence diagrams for <spec-id>"
   ```
5. **API Documentation Summary** — Present a concise documentation update report back to the team:
   - New paths and endpoints documented.
   - Response models and request body parameters added.
   - Relative markdown links to `docs/api/openapi.yaml` and the updated sequence diagrams.

## Project Context

- **Project:** appteam
