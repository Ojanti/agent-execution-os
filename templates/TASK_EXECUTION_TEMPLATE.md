# Task: [Task Name]

```yaml
risk_class: R0 | R1 | R2
allowed_paths:
  - "[path/glob/**]"
approved_dependency_change: false
approved_destructive: false
requires_clean_checkout: false
requires_r2_review: false
```

## Purpose

[Explain why this task exists and what outcome it enables.]

## Required reading

Before execution, read:

1. `/docs/agent/14_WORKER_STANDARDS_CARD.md`
2. This task file fully, twice
3. Any files explicitly listed below

Do not read the full project overview unless explicitly instructed.

## Context summary

[Give enough local project/phase context for the worker to execute safely without broad project history.]

## User inputs required

[If none, say: None.]

If input is needed, include:

- what is needed
- why it is needed
- how to get it, step by step
- where to provide it
- safety warning, if relevant
- what happens next

## Files/areas likely involved

- [File/area]

## Allowed paths

The worker may edit only:

- `[path/glob/**]`

If implementation requires editing outside these paths, stop and report.

## Required implementation

1. [Specific step]
2. [Specific step]
3. [Specific step]

## Non-goals

- [What not to do]

## Security rules

- [Specific security rule]

## Data/model rules

- [Specific data rule]

## UX rules, if relevant

- [Specific UX rule]

## Testing requirements

- [Specific test requirement]

## Acceptance criteria

- [ ] [Checkable criterion]
- [ ] [Checkable criterion]

## Verification commands

Run and capture raw output + exit code:

```bash
[command]
```

```bash
[command]
```

## Stop conditions

Stop and report if:

- required metadata is missing
- required user input is missing
- implementation requires edits outside `allowed_paths`
- implementation requires dependency changes and `approved_dependency_change` is false
- implementation requires destructive changes and `approved_destructive` is false
- verification fails and cannot be fixed within scope
- instructions conflict
- security would need to be weakened

## Reporting section

### Scope check

| Changed file | Inside allowed_paths? | Notes |
|---|---:|---|
| [file] | Yes/No | [notes] |

### Files changed

- [file]

### Implementation summary

- [summary]

### Acceptance criteria results

| Criterion | Result | Evidence/notes |
|---|---|---|
| [criterion] | Pass/Fail | [notes] |

### Verification results

| Check | Command/method | Exit code | Result | Evidence excerpt |
|---|---|---:|---|---|
| [check] | `[command]` | [code] | Pass/Fail/Skipped | [output] |

### Risks / follow-ups

- [risk/follow-up]

### Commit message

`[type/scope: message]`
