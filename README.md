# 🤖 Scion AppTeam

> **An Autonomous, Multi-Agent Software Development Team Orchestrated by Scion**

[![Scion Compatible](https://img.shields.io/badge/Scion-Compatible-brightgreen.svg?style=flat-square)](https://github.com/gitrey/scion-appteam)
[![Orchestration](https://img.shields.io/badge/Orchestration-Containerized-blue.svg?style=flat-square)]()
[![License](https://img.shields.io/badge/License-MIT-orange.svg?style=flat-square)]()

`scion-appteam` is an advanced, fully containerized multi-agent simulation
environment designed for autonomous software engineering. Rather than relying on
a single monolithic LLM context, it models a professional, role-based agile
software development team using specialized agents working in concert.

---

## 🎯 Project Goal

The primary goal is **autonomous end-to-end feature delivery, code quality
assurance, and project tracking**. By dividing complex engineering operations
into isolated roles (Product Management, Architecture, Engineering, Testing, and
Review), `scion-appteam`:

- **Eliminates context bloating** by keeping each agent focused strictly on
  their domain.
- **Enforces professional workflows** (specs are approved before coding begins,
  code is tested before review).
- **Enables parallel implementation** using isolated Git worktrees and
  containerized environments.

---

## 🏗️ Team Architecture & Workflow

The project simulates a complete agile lifecycle through specialized agent personas interacting via defined messaging interfaces and JIRA:

```mermaid
graph TD
    User["👤 User (Product Owner / CEO)"] -->|1. /pipeline Feature Request| PM["📋 Product Manager (PM)"]
    
    subgraph "Planning & Backlog"
        PM -->|2. Requests JIRA Stories| PO["⚙️ PO Agent (Atlassian MCP)"]
        PO -->|3. Creates & Grooms Issues| JIRA[("JIRA Board")]
        PM -->|4. Creates Product Spec| Spec[("docs/specs/")]
        PM -->|5. Hands off Spec & JIRA IDs| TPM["⚙️ Technical Product Manager (TPM)"]
        TPM -->|6. Populates Backlog| Backlog[("docs/BACKLOG.md")]
    end
    
    subgraph "Implementation & Verification"
        TPM -->|7. Assigns Tasks| SWE1["💻 SWE-1"]
        TPM -->|7. Assigns Tasks| SWE2["💻 SWE-2"]
        SWE1 -->|8. Transitions JIRA & Writes Code| Codebase["🛠️ Workspace Code"]
        SWE2 -->|8. Transitions JIRA & Writes Code| Codebase
        Codebase -->|9. Verifies Code Quality| Test["🧪 SWE-Test"]
        Codebase -->|9. Verifies Visual Layout| UITest["🎨 ui-test (Chrome DevTools)"]
        Codebase -->|9. Verifies Performance| Perf["⚡ perf-test (Locust)"]
        UITest -->|10. Captures Screenshots| Screenshots[("docs/screenshots/")]
        Perf -->|10. Generates Reports| PerfReports[("docs/perf-reports/")]
        Test -->|11. Opens PR referencing JIRA ID| PR["GitHub Pull Request"]
        UITest -->|11. Links Screenshots in PR| PR
        Perf -->|11. Links Performance in PR| PR
    end
    
    subgraph "Quality Assurance & Release"
        PR -->|12. Reviews PR & Approves| Reviewer["🔍 Reviewer"]
        Reviewer -->|13. Triggers Deployment| DevOps["🛠️ DevOps Agent"]
        DevOps -->|14. Provisions & Deploys| GCP[("Google Cloud (Cloud Run/GKE)")]
        DevOps -->|15. Releases Milestone| Release["📄 docs/RELEASENOTES.md"]
        Release -->|16. Reports Completion| PM
        PM -->|17. Delivers Summary| User
    end
```

### 👥 The Personas

1. **👤 Product Owner (PO)**: Manages the JIRA backlog, creates and grooms issues using native Atlassian MCP tools, and represents the voice of business/stakeholders.
2. **📋 Product Manager (PM)**: Bridges the PO's feedback/requests and the technical team. Focuses on creating specs under `docs/specs/` and detailing acceptance criteria.
3. **⚙️ Technical Product Manager (TPM)**: Manages `docs/BACKLOG.md` and orchestrates SWE assignments, priority, and task completion.
4. **💻 Software Engineers (SWE-1 & SWE-2)**: Specialize in direct codebase implementation, resolving requirements according to approved specs on feature branches, and opening PRs via `gh` CLI.
5. **🧪 Software Engineer Test (SWE-Test)**: Responsible for generating unit, integration, and end-to-end tests to verify acceptance criteria.
6. **🎨 UI Test Automation Agent (ui-test)**: Specializes in automated browser testing, DOM/CSS inspection, visual verification, and screenshot audits using the Chrome DevTools MCP.
7. **⚡ Performance Testing Engineer Agent (perf-test)**: Specializes in concurrent traffic simulation (Locust), scalability audits, response time/latency profiling (p50, p95, p99), and performance metrics reporting.
8. **🛠️ DevOps Engineer Agent (devops)**: Specializes in declarative infrastructure provisioning (Terraform), container orchestration (Kubernetes YAML), and secure automated cloud deployments (using `gcloud` to Cloud Run).
9. **🔍 Reviewer**: Performs comprehensive code reviews, grants approvals, and reviews Pull Requests via `gh` CLI, leaving final merges for human engineers.

---

## 📂 Project Structure

```typescript
scion-appteam/
├── .scion/                  // Scion orchestration settings
│   └── templates/           // Agent templates & custom prompts
│       ├── po/              // Product Owner configuration, system prompt & JIRA skills
│       │   └── skills/      // PO JIRA skills (/story, /groom)
│       ├── pm/              // Product Manager configurations & skills
│       ├── reviewer/        // Reviewer configurations & skills
│       ├── swe-1/           // Software Engineer 1 configurations & skills
│       ├── swe-2/           // Software Engineer 2 configurations & skills
│       ├── swe-test/        // QA/Testing configurations & skills
│       ├── ui-test/         // UI Test Automation Agent configuration, prompt & skills
│       │   └── skills/      // UI Test skills (/visual-verify)
│       ├── devops/          // DevOps Engineer Agent configuration, prompt & skills
│       │   └── skills/      // DevOps skills (/deploy, /logs)
│       ├── perf-test/       // Performance Testing Agent configuration, prompt & skills
│       │   └── skills/      // Performance skills (/locust)
│       └── tpm/             // Technical Product Manager configurations & skills
├── docs/                    // Shared documentation & agile tracking
│   ├── specs/               // Feature specifications & requirements
│   ├── adr/                 // Architecture Decision Records
│   ├── BACKLOG.md           // Global product backlog
│   ├── PROGRESS.md          // Active work item status
│   ├── RELEASENOTES.md      // Completed milestones & version history
│   └── perf-reports/        // Headless Locust performance HTML reports
└── README.md                // Project overview (this file)
```

---

## 🛠️ Key Agent Skills

Each agent template is equipped with specialized `/` skills designed to automate common software processes:

- **`/story`** (PO): Automates creation of highly-structured JIRA stories and bugs with testable acceptance criteria via the Atlassian MCP server.
- **`/groom`** (PO): Performs comprehensive JIRA backlog grooming, auditing ticket descriptions, and refining priorities dynamically.
- **`/visual-verify`** (ui-test): Automates end-to-end visual QA and browser interactions, capturing state screenshots via Chrome DevTools MCP.
- **`/locust`** (perf-test): Executes headless Locust load tests simulating high concurrent user traffic, profiling response time latencies (p50, p95, p99) non-interactively.
- **`/deploy`** (devops): Builds container images, provisions GCP infrastructure via Terraform, and deploys microservices to Cloud Run non-interactively.
- **`/logs`** (devops): Automatically queries and audits application logs from Cloud Run or GKE pods to isolate technical blockers.
- **`/pipeline`** (PM/TPM/SWE): Spins up the full agent team, creates tasks, and initiates the structured workflow in dedicated execution panes.
- **`/adr`** (SWE-Test/PM/Reviewer): Automates the creation of Architecture Decision Records under `docs/adr/` with standard templates.
- **`/regenerate`** (PM): Reads project configurations from `.appteam/settings.json` and automatically regenerates template structures while preserving core tracking files.
- **`/release`** (PM): Automates release note aggregation and version tagging upon milestone completion.

---

## 🚀 Getting Started

### 1. Initialize the Environment

Set up your Scion workspace:

```bash
scion init
```

### 2. Trigger the Pipeline

Spawn the entire autonomous development team with a specific feature target:

```bash
# Initiates the autonomous agile flow for a new feature
/pipeline "Implement dark mode support across the application"
```

### 3. Document Architectural Decisions

To propose a new architectural change:

```bash
/adr "Use PostgreSQL for order management persistence"
```

---

_Developed with 🦾 using the
[Scion Framework](https://github.com/gitrey/scion-appteam)._
