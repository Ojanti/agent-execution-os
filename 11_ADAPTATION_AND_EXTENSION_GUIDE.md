# 11. Adaptation and Extension Guide

## Purpose

Agent Execution OS is reusable, but it must be adapted for every project.

The base system is intentionally robust. Project packs should inherit it, then extend or modify expectations where needed.

## Core principle

```text
Base OS first. Project-specific extension second.
```

## What must never be removed

These rules are core:

- do not commit secrets
- do not weaken security to pass tests
- do not broaden task scope without approval
- every task must define acceptance criteria
- every task must define verification commands
- every task must define stop conditions
- every task must report what changed and what was verified
- every user request must explain how to get what is needed
- every user-facing communication must say what happens next

## What should be customized

Every project should customize:

- quality bar
- testing expectations
- UX expectations
- accessibility expectations
- security guardrails
- deployment environments
- code conventions
- data conventions
- third-party provider rules
- performance budgets
- monitoring/analytics requirements
- AI cost/provider rules, if relevant

## Adaptation checklist

Before execution, complete this checklist:

```md
## Project Adaptation Checklist

### Project identity
- Project name:
- Project type:
- Business goal:
- Technical goal:
- Target users:
- Risk level:

### Architecture
- Main stack:
- Database:
- Auth:
- Hosting:
- External services:
- AI providers, if any:

### Environments
- Local:
- Staging:
- Production:

### Quality extensions
- TypeScript rules:
- Testing rules:
- UX rules:
- Accessibility rules:
- Performance rules:
- Documentation rules:

### Security extensions
- Auth rules:
- Tenancy rules:
- Data privacy rules:
- Billing rules:
- Webhook/cron rules:
- Logging/redaction rules:

### Roadmap
- Sections:
- First section:
- First phase:
- First execution pack:

### User inputs likely required
- Accounts:
- Keys/secrets:
- Domains:
- Product decisions:
- Sample data:
```

## Customizing the quality bar

Base quality bar should be extended per project.

Example for SaaS:

```md
## Project-Specific Quality Extension: SaaS

- All user-owned data must be scoped by authenticated user or tenant.
- Billing status must come from server/webhook state.
- Staging must not point to production database.
- Every private API route must have auth tests or documented manual verification.
```

Example for design system:

```md
## Project-Specific Quality Extension: Design System

- Component changes require Storybook coverage.
- Token changes require before/after documentation.
- Accessibility behavior must be documented for interactive components.
- Breaking API changes require migration notes.
```

Example for AI automation product:

```md
## Project-Specific Quality Extension: AI Product

- Prompts that affect product behavior must be versioned.
- Model calls must have cost/rate controls.
- AI outputs persisted to DB must be validated.
- Evaluation cases must be updated when scoring/routing logic changes.
```

## Template customization markers

Use these markers in project-pack templates:

```md
<!-- DO NOT REMOVE: core Agent Execution OS rule -->
<!-- REQUIRED: replace this section for every project -->
<!-- EXTEND: add project-specific rules here -->
<!-- OPTIONAL: delete if not relevant -->
```

## Optional modules

Enable optional modules only when relevant.

Examples:

- Billing module
- Multi-tenancy/RLS module
- Mobile app release module
- Chrome extension module
- AI evaluation module
- Design token module
- Internationalization module
- Support/ops module

## Example: adapting to a consumer SaaS AI app

```text
Project type: Consumer SaaS / AI curation product
Risk level: High
Quality extensions: tenant isolation, delivery logs, AI cost controls, onboarding UX
Security extensions: auth, RLS, service-role boundaries, webhook verification
First execution pack: foundation, staging/prod, auth, tenancy, RLS
```

## Example: adapting to a design system project

```text
Project type: Design system / component library
Risk level: Medium
Quality extensions: Storybook, visual regression, accessibility, API docs
Security extensions: package publishing secrets, CI release gates
First execution pack: token architecture, component API standards, release process
```

## Example: adapting to an internal automation tool

```text
Project type: Internal automation / workflow tool
Risk level: Medium-high
Quality extensions: worker reliability, retry behavior, logs, manual override
Security extensions: admin access, secret management, provider scopes
First execution pack: environment setup, queue/worker safety, observability
```

## How much to detail upfront

Use this rule:

```text
Current section: full task detail
Next section: phase-level detail
Later sections: roadmap outline
```

Do not fully detail every future task too early. Architecture changes during early phases can make later task docs stale.

## What to do when the project changes

When major decisions change:

1. Update Architecture Decisions.
2. Update Roadmap Index.
3. Update affected Section Briefs.
4. Update affected Phase Briefs.
5. Rewrite task files only when they are near execution.
6. Update status files.

## Final adaptation rule

If the project has special risk, encode it into the docs before execution.

Do not rely on agents to infer special standards from vibes.
