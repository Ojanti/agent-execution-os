# Fix Task: [Issue]

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

Fix a specific failed check or rejected task result. Do not broaden scope.

## Source of failure

- Original task:
- Failed check:
- Evidence:
- Supervisor instruction:

## Required reading

1. `/docs/agent/14_WORKER_STANDARDS_CARD.md`
2. Original task file
3. Failed report/gate evidence
4. This fix task

## Required fix

1. [Specific fix]
2. [Specific fix]

## Non-goals

- Do not revisit unrelated parts of the original task.
- Do not refactor beyond the failed area.
- Do not change acceptance criteria unless Supervisor/Director approves.

## Verification

Run and capture raw output + exit code:

```bash
[command]
```

## Reporting section

### Files changed

- [file]

### Fix summary

- [summary]

### Verification evidence

| Check | Command/method | Exit code | Result | Evidence excerpt |
|---|---|---:|---|---|
| [check] | `[command]` | [code] | Pass/Fail | [output] |

### Remaining issues

- [issue]

### Commit message

`fix: [message]`
