# Spec: F-0006-hr-agent-onboarding

- **Title:** Introduce HR Agent Configuration and Team Protocol Enforcement
- **Type:** Enhancement
- **Priority:** P2
- **Status:** Approved
- **Requested by:** PM
- **Date:** 2026-05-08
- **JIRA ID:** GENDEV-105

## Problem
The team needs a dedicated role for onboarding, health monitoring, and protocol enforcement to ensure long-term stability and prevent the friction points identified in Milestone 4.

## Requirements
1. **HR Agent Persona**: Define and implement a new agent template for HR.
2. **Team Protocols**: Formalize the non-interactive git and sync requirements.
3. **Onboarding Documentation**: Update the README and project structure to include the new role.

## Acceptance Criteria
- [x] HR agent template created in `.scion/templates/hr/`.
- [x] All agent prompts updated with synchronization and non-interactive rules.
- [x] README updated with HR persona description.
- [x] Protocols documented in `docs/protocols.md`.

## Out of Scope
- Automated HR performance reviews.

## Dependencies
- F-0005: Milestone 4 Retrospective Action Items
