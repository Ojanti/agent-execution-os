# 15. Task File Readiness Rubric

## Purpose

Weak task files create weak execution. This rubric defines when a task is ready to hand to a worker.

A task that fails readiness should not be dispatched.

## Core rule

```text
Definition of Ready comes before Definition of Done.
```

## Readiness checklist

A task is ready only if it includes all required items below.

### 1. Purpose

The task explains why it exists and what outcome it enables.

Bad:

```text
Fix auth.
```

Good:

```text
Add authenticated route protection to the app shell so signed-out users cannot access private inbox routes. Do not implement RLS in this task.
```

### 2. Risk metadata

The task includes:

```yaml
risk_class: R0 | R1 | R2
allowed_paths:
  - "..."
approved_dependency_change: false
approved_destructive: false
requires_clean_checkout: false
requires_r2_review: false
```

### 3. Context summary

The task contains enough local context for a worker to execute without reading the whole project history.

It explains:

- phase context
- current behavior
- target behavior
- relevant constraints

### 4. Required reading

The task lists exact documents/files to read.

Default:

```text
1. /docs/agent/14_WORKER_STANDARDS_CARD.md
2. This task file fully, twice
3. Files explicitly listed by this task
```

### 5. User inputs

The task says whether user input is required.

If required, it includes:

- what is needed
- why it is needed
- how the user gets it
- where the user provides it
- safety warning
- what happens next

If none, it says:

```text
None.
```

### 6. Allowed paths

The task declares what paths may be edited.

This should be a positive allowlist, not only a denylist.

### 7. Implementation steps

Steps are specific enough for a weaker worker.

Bad:

```text
Improve the UI.
```

Good:

```text
Replace hardcoded card background classes in `src/components/job-card/**` with semantic shadcn/Tailwind variables: `bg-card`, `text-card-foreground`, `border-border`. Do not change layout or copy.
```

### 8. Non-goals

The task clearly says what not to do.

Examples:

- do not add billing
- do not change scoring logic
- do not change navigation
- do not add dependencies
- do not refactor unrelated components

### 9. Acceptance criteria

Acceptance criteria are checkable.

Bad:

```text
Looks better.
```

Good:

```text
- [ ] No user-facing raw strings remain in the edited component.
- [ ] Component uses semantic classes instead of hardcoded gray/white colors.
- [ ] Loading, empty, and error states are preserved.
```

### 10. Verification commands

The task provides exact commands or says why none are needed.

Each command must require raw output and exit code in the report.

### 11. Stop conditions

The task lists when the worker must stop.

Examples:

- needs to edit outside allowed paths
- requires dependency change not approved
- requires destructive migration not approved
- missing required key/account/data
- tests fail for unrelated reasons
- security rule conflict

### 12. Reporting section

The task contains a report template the worker must fill.

## Readiness scoring

| Score | Meaning | Action |
|---:|---|---|
| 0 | Missing purpose or scope | Rewrite task |
| 1 | Vague and risky | Rewrite task |
| 2 | Mostly clear but missing metadata/verification | Fix before dispatch |
| 3 | Ready for R0/R1 | Dispatch |
| 4 | Ready for R2 | Dispatch with stricter gates |

## Supervisor responsibility

The Supervisor must not launch a worker on a task that fails readiness.

If a task is not ready, the Supervisor should either:

- fix the task file
- ask Director/user for missing inputs
- split the task
- escalate if scope is unclear

## Split conditions

Split a task if it:

- touches unrelated systems
- mixes audit, implementation, and verification too heavily
- requires multiple independent commits
- combines R0/R1 work with R2 work unnecessarily
- cannot be reverted independently
- cannot be verified independently
- requires major design/product approval mid-task

## Final readiness rule

```text
A task file should make worker success boring.
```
