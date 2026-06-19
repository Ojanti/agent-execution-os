# 02. Document System

## Purpose

The document system turns project context into executable instructions for AI agents.

It has three levels:

```text
Operating System docs
Project Pack docs
Execution docs
```

## Operating System docs

These are reusable across projects.

```text
README.md
01_OPERATING_MODEL.md
02_DOCUMENT_SYSTEM.md
03_DOCUMENT_CREATION_PROTOCOL.md
04_COMMUNICATION_PROTOCOL.md
05_QUALITY_BAR.md
06_SECURITY_GUARDRAILS.md
07_TASK_GRANULARITY_RULES.md
08_PHASE_PREFLIGHT_PROTOCOL.md
09_PARALLELIZATION_PROTOCOL.md
10_REPORTING_AND_STATUS_PROTOCOL.md
11_ADAPTATION_AND_EXTENSION_GUIDE.md
```

They define how the system works.

## Project Pack docs

These are generated/customized for a specific project.

```text
/docs/agent/
  00_PROJECT_OVERVIEW.md
  01_DIRECTOR_OPERATING_MANUAL.md
  02_SUPERVISOR_OPERATING_MANUAL.md
  03_SUBAGENT_EXECUTION_RULES.md
  04_QUALITY_BAR.md
  05_SECURITY_GUARDRAILS.md
  06_ARCHITECTURE_DECISIONS.md
  07_ROADMAP_INDEX.md
  08_TASK_TEMPLATE.md
  09_PHASE_BRIEF_TEMPLATE.md
  10_SUPERVISOR_REPORT_TEMPLATE.md
```

## Execution docs

These exist inside project sections.

```text
/docs/agent/sections/
  01_section_name/
    SECTION_BRIEF.md
    PHASES.md
    phase-01-phase-name/
      PHASE_BRIEF.md
      01_task-name.md
      02_task-name.md
      03_phase-verification-gate.md
```

## Status docs

These preserve continuity across agent sessions.

```text
/docs/agent/status/
  ROADMAP_STATUS.md
  DECISIONS_LOG.md
  BLOCKERS.md
  SECTION_01_STATUS.md
```

## File responsibility matrix

| File | Primary reader | Purpose |
|---|---|---|
| `00_PROJECT_OVERVIEW.md` | Director, Supervisors | Full project context |
| `01_DIRECTOR_OPERATING_MANUAL.md` | Director | Director behavior and limits |
| `02_SUPERVISOR_OPERATING_MANUAL.md` | Supervisors | Section coordination rules |
| `03_SUBAGENT_EXECUTION_RULES.md` | Subagents | Worker behavior and limits |
| `04_QUALITY_BAR.md` | All actors | Definition of done |
| `05_SECURITY_GUARDRAILS.md` | All actors | Non-negotiable safety rules |
| `06_ARCHITECTURE_DECISIONS.md` | Director, Supervisors, some Subagents | Existing decisions |
| `07_ROADMAP_INDEX.md` | Director, Supervisors | Project roadmap |
| `SECTION_BRIEF.md` | Supervisor | Section context and done criteria |
| `PHASE_BRIEF.md` | Supervisor, sometimes Subagents | Phase context, preflight, dependencies |
| task file | Subagent | Source of truth for execution |

## Section → Phase → Task

Use this hierarchy for all non-trivial projects.

### Section

A section is a major product/engineering pillar.

Examples:

- Foundation, Environments, Auth & Security
- Consumer Data Model & Inbox
- Delivery Intelligence
- Billing & Usage Metering
- Support & Observability

### Phase

A phase is a meaningful milestone within a section.

Examples:

- Staging/Production Separation
- Auth & Tenancy
- RLS Implementation
- Email Digest v1
- Stripe Billing Test Mode

### Task

A task is an executable unit for one subagent.

Examples:

- Audit environment variables and classify them by environment
- Add typed env validation and fail-fast config
- Create staging seed script with fake users
- Add regression tests proving tenant isolation

## What belongs where

### Project Overview

Global context. Do not turn it into task instructions.

### Section Brief

Section-level purpose, risks, phase list, and completion criteria.

### Phase Brief

Phase-level preflight, user inputs, task dependency map, and phase done criteria.

### Task File

Detailed executable instructions.

The task file is where specificity lives.

## Anti-patterns

### Bad: giant task file

```text
01_implement-staging-production-auth-billing-and-notifications.md
```

This is not a task. It is a project.

### Bad: vague task file

```text
Add auth.
```

No context, no acceptance criteria, no verification, no boundaries.

### Good: clear task file

```text
04_add-authenticated-app-route-guard.md
```

With clear scope, files, non-goals, acceptance criteria, verification, and reporting.

## Documentation depth rule

Document deeply where execution is near.

```text
Current section: very detailed
Next section: medium detail
Later sections: roadmap/detail-light
```

Do not produce 80 fully detailed task files too early. But do define all proposed sections and phases upfront.

## v1.1 additions

The document system now includes a truth layer:

```text
12_RISK_CLASS_AND_ROUTING.md
13_VERIFICATION_GATE_PROTOCOL.md
14_WORKER_STANDARDS_CARD.md
15_TASK_FILE_READINESS_RUBRIC.md
16_OPTIONAL_ENFORCEMENT_ADAPTERS.md
```

Execution tasks must declare risk class, allowed paths, approval flags, verification evidence requirements, and stop conditions.
