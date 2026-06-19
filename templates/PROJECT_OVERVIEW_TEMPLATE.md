# [Project Name] — Project Overview

<!-- REQUIRED: replace all bracketed placeholders before execution. -->

## Purpose of this document

This document onboards Director and Supervisor agents into the project.

It explains the business goal, technical context, current state, target state, architecture, risks, standards, and how to use the execution document set.

Subagents should not read this full document by default. Subagents should read their task file plus required standards unless explicitly instructed otherwise.

## Project identity

- Project name: [Name]
- Project type: [Consumer SaaS / B2B SaaS / mobile app / design system / AI automation / etc.]
- Primary users: [Users]
- Business goal: [Goal]
- Technical goal: [Goal]
- Current status: [Prototype / internal tool / beta / production / migration]
- Risk level: [Low / Medium / High]

## What this product/project is

[Explain clearly.]

## What this product/project is not

[Define scope boundaries.]

## Current state

[Describe existing codebase/product/architecture.]

## Target state

[Describe where the project should land after this roadmap.]

## Core principles

1. [Principle]
2. [Principle]
3. [Principle]

## Current architecture

### Stack

- Frontend:
- Backend:
- Database:
- Auth:
- Hosting:
- Background jobs:
- External services:
- AI providers:

### Main data flow

```text
[Input]
↓
[Processing]
↓
[Storage]
↓
[User-facing output]
```

## Known risks

| Risk | Severity | Notes |
|---|---|---|
| [Risk] | [Low/Med/High] | [Notes] |

## Non-negotiable guardrails

<!-- DO NOT REMOVE: core Agent Execution OS rule -->

- Do not commit secrets.
- Do not weaken security to pass tests.
- Do not broaden task scope without approval.
- Every user request must explain how to get what is needed.
- Every user-facing communication must say what happens next.

<!-- EXTEND: add project-specific guardrails. -->

## Coding standards

[Project-specific coding standards.]

## Testing standards

[Project-specific testing standards and commands.]

## UX standards

[Project-specific UX expectations.]

## Security standards

[Project-specific security expectations.]

## Deployment/environments

```text
Local:
Staging:
Production:
```

## Actor model

```text
Director reads the world.
Supervisor reads the section and tracks phases + task progression.
Subagent reads the task + standards and executes.
```

## How to use this document set

- Director reads this document before roadmap decisions.
- Supervisors read this document before section execution.
- Subagents do not read this document unless instructed by the task.
- Task files are the source of truth for implementation.

## Links/references

- Repo:
- Staging:
- Production:
- Design:
- Docs:
- Analytics:
- Error tracking:
