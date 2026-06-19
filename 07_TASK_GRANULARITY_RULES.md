# 07. Task Granularity Rules

## Purpose

This document defines how to break large work into executable units for AI subagents.

Poor granularity creates poor execution.

## Hierarchy

```text
Section → Phase → Task
```

## Section

A section is a major pillar.

Good section examples:

- Foundation, Environments, Auth & Security
- User Profile & Onboarding
- Delivery Intelligence
- Billing & Usage Metering
- Support & Observability

A section is owned by one Supervisor.

## Phase

A phase is a milestone within a section.

Good phase examples:

- Staging/Production Separation
- Auth & Tenancy
- Notification Preferences Model
- Email Digest v1
- Stripe Test Mode Setup

A phase has a `PHASE_BRIEF.md` and multiple tasks.

## Task

A task is an executable unit for one subagent.

A good task:

- has one clear outcome
- touches a limited file area
- can be verified independently
- can be committed independently
- can be reverted independently
- has clear acceptance criteria
- has clear stop conditions
- does not require major product judgment mid-task

## Bad task examples

```text
Implement auth, tenancy, and RLS.
```

Too broad. Split it.

```text
Build notifications.
```

Too vague. Split by model, scheduling, channel, delivery log, unsubscribe, verification.

```text
Make the app production ready.
```

Not a task. It is a roadmap.

## Good task examples

```text
Audit all current database tables and classify each as global, system-owned, user-owned, or derived/cache.
```

```text
Add typed environment validation and update `.env.example` without changing deployment configuration.
```

```text
Implement RLS policies for `saved_jobs` and add tests proving User A cannot read User B rows.
```

```text
Create email digest renderer for already-selected inbox items, without changing scoring or routing logic.
```

## Split a task when it includes multiple verbs

Bad:

```text
Audit environment variables, add validation, configure Vercel, create staging seed data, and verify deployment.
```

Split into:

```text
01_environment-inventory.md
02_environment-contract-and-validation.md
03_vercel-project-separation.md
04_seed-data-and-test-accounts.md
05_staging-deployment-verification.md
```

## Split a task when it crosses subsystems

If a task touches database, API, UI, billing, and notifications, it is probably too big.

## Split audit from implementation

Audits produce findings and recommendations.
Implementation applies a specific decision.

Bad:

```text
Audit and fix all security issues.
```

Good:

```text
01_route-protection-audit.md
02_add-auth-guards-to-private-routes.md
03_add-cron-secret-verification.md
04_security-regression-gate.md
```

## Split schema from policy from application refactor

Bad:

```text
Make database multi-tenant.
```

Good:

```text
01_table-ownership-classification.md
02_add-user-ownership-columns.md
03_add-rls-policies.md
04_refactor-user-scoped-queries.md
05_tenant-isolation-tests.md
```

## Verification gates

Every phase should end with a verification task.

Example:

```text
08_phase-verification-gate.md
```

This task should:

- run all relevant checks
- review all reports
- confirm acceptance criteria
- identify unresolved risks
- mark phase complete or blocked

## Task size target

A task should usually be completable by one subagent in one focused session.

Prefer 5 small safe tasks over 1 massive ambiguous task.

## Independence rule

A task should produce a coherent commit.

If the commit message would need “and also,” the task may be too broad.

## Dependency clarity

Every task should state:

- can run immediately
- depends on task X
- blocks task Y
- can run in parallel with tasks A/B

This can live in the phase brief rather than repeated in every task.

## User input clarity

If a task needs user input, the task must specify:

- exact input needed
- how to get it
- where to put it
- safety warning
- what happens next

## Quality threshold

A task file is not ready for subagent execution until it has:

- purpose
- context
- required reading
- scope
- non-goals
- step-by-step implementation
- acceptance criteria
- verification commands
- stop conditions
- report section
