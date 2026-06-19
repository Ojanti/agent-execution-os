# 12. Risk Class and Routing

## Purpose

Risk classes make Agent Execution OS proportional. A typo fix should not carry the same ceremony as auth, billing, RLS, production configuration, or destructive migrations.

The goal is not bureaucracy. The goal is to route the right work to the right actor, verification depth, and review standard.

## Core rule

```text
Classify by blast radius. If unsure, classify upward.
```

Every executable task must declare:

```yaml
risk_class: R0 | R1 | R2
allowed_paths:
  - "path/or/glob/**"
approved_dependency_change: false
approved_destructive: false
requires_clean_checkout: false
requires_r2_review: false
```

## Risk classes

### R0: Mechanical / low risk

Use R0 for tiny, reversible work with narrow blast radius.

Examples:

- documentation edits
- renaming a local variable
- adding a small pure helper
- adding a test around existing behavior
- updating copy in translation files
- adding a non-invasive UI state within an existing pattern

Expected overhead:

- worker may execute directly from a ready task file
- standard verification evidence required
- no separate reviewer required unless the task says so

### R1: Standard feature work

Use R1 for normal product or engineering work that is recoverable but meaningful.

Examples:

- adding a new UI component
- adding a non-admin API endpoint
- adding a non-destructive migration
- refactoring a bounded module
- adding a notification preference screen
- implementing a standard integration in test mode

Expected overhead:

- task must pass Definition of Ready
- `allowed_paths` must be explicit
- evidence-backed verification required
- supervisor review required
- phase verification gate later re-checks the combined work

### R2: Dangerous / security-sensitive / irreversible

Use R2 for work that can leak data, break billing, damage production, bypass authorization, create hidden cost exposure, or make destructive changes.

Examples:

- authentication
- authorization
- tenant isolation
- Supabase RLS
- billing and subscriptions
- payment webhooks
- secrets and key handling
- production environment configuration
- cron/admin endpoints
- destructive migrations
- public AI-cost-triggering paths
- service-role/server-only boundaries
- data deletion/export/privacy flows

Expected overhead:

- classify upward when mixed with lower-risk work
- explicit user/operator approval for destructive or dependency changes
- clean-checkout verification required
- R2 reviewer required for high-risk production/security work unless explicitly waived and logged
- worker may not author or modify the tests that grade the R2 security behavior unless the task explicitly permits it

## Mixed tasks

A task containing multiple risk levels inherits the highest risk.

Bad:

```text
This is mostly UI, but it also adjusts auth middleware, so call it R1.
```

Good:

```text
This touches auth middleware, so it is R2.
```

## Routing rules

| Risk | Worker | Supervisor review | Clean checkout | Independent reviewer | Waiver allowed? |
|---|---|---:|---:|---:|---:|
| R0 | cheapest reliable worker | optional | no | no | n/a |
| R1 | cheapest reliable worker | yes | phase gate only | no, unless specified | yes |
| R2 | reliable worker under strict scope | yes | yes | yes for prod/security, unless waived | yes, logged |

## Role-based model binding

Agent Execution OS core never hardcodes model names.

Core roles:

```text
director
supervisor
worker
r2_reviewer
```

Concrete model choices belong in a project or adapter file, such as:

```text
optional/cursor-enforcement/model-bindings.yaml
```

Guidance:

- use the cheapest reliable executor for workers
- use a stronger reviewer/director for high-risk review and planning
- keep bindings configurable per project
- log overrides and waivers

## Scope allowlist

Every task must define what the worker may edit.

```yaml
allowed_paths:
  - "src/app/inbox/**"
  - "src/components/job-card/**"
  - "messages/en.json"
```

The worker must stop and report if implementation requires edits outside the allowlist.

Allowed paths are stronger than forbidden paths. A denylist is always incomplete. A positive allowlist makes drift visible and mechanically checkable.

## Approval flags

### Dependency changes

Default:

```yaml
approved_dependency_change: false
```

If a dependency or lockfile change is needed, the task must explicitly approve it and explain why.

### Destructive changes

Default:

```yaml
approved_destructive: false
```

Destructive migrations, data deletion, production resets, or irreversible operations require explicit approval.

## Artifact blocking vs operator control

Security gates may block an artifact. They must never lock out the operator.

```text
Gates block the commit/merge/artifact.
The human/operator decides what happens next.
```

A blocked artifact is like a failing test: fix, waive with cause, or re-scope. It is not an auto-kill switch.

## Required task metadata

Every execution task must include:

```yaml
risk_class: R0 | R1 | R2
allowed_paths:
  - "..."
approved_dependency_change: false
approved_destructive: false
requires_clean_checkout: false
requires_r2_review: false
```

If metadata is missing, the task is not ready.
