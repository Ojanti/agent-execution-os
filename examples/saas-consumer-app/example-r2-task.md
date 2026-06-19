# Task: Implement user-owned inbox RLS policies

```yaml
risk_class: R2
allowed_paths:
  - "supabase/migrations/**"
  - "src/server/db/**"
  - "tests/rls/**"
approved_dependency_change: false
approved_destructive: false
requires_clean_checkout: true
requires_r2_review: true
```

## Purpose

Add RLS policies that prevent one user from reading or mutating another user's inbox records.

## Required reading

1. `/docs/agent/14_WORKER_STANDARDS_CARD.md`
2. Current phase brief
3. Current schema/migration files

## Context summary

The product is becoming a multi-user SaaS. Inbox records are user-owned. User A must never read User B's inbox data.

## User inputs required

None.

## Required implementation

1. Inspect inbox-related tables.
2. Add RLS policies for select/insert/update/delete where applicable.
3. Ensure policies use authenticated user identity.
4. Add tests proving User A cannot access User B records.
5. Do not change billing, scoring, or notification logic.

## Non-goals

- Do not redesign the inbox UI.
- Do not implement onboarding.
- Do not add dependencies.
- Do not create destructive migrations.

## Acceptance criteria

- [ ] RLS enabled on user-owned inbox tables.
- [ ] User A cannot read User B inbox records.
- [ ] User A cannot mutate User B inbox records.
- [ ] Server-only/service-role boundaries are not weakened.
- [ ] Tests include both allowed and denied access cases.

## Verification commands

Run and capture raw output + exit code:

```bash
pnpm test:rls
```

```bash
pnpm typecheck
```

## Stop conditions

Stop if implementation requires destructive schema changes, dependency changes, or broad app query refactors outside allowed paths.

## Reporting section

[Use `TASK_EXECUTION_TEMPLATE.md` reporting format.]
