# Task: Phase Verification Gate — [Phase Name]

```yaml
risk_class: R1 | R2
allowed_paths:
  - "docs/agent/status/**"
  - "[phase/report paths]"
approved_dependency_change: false
approved_destructive: false
requires_clean_checkout: true
requires_r2_review: [true/false]
```

## Purpose

Verify that the combined output of the phase is safe, scoped, documented, and ready for Director approval.

## Required reading

1. `/docs/agent/14_WORKER_STANDARDS_CARD.md`
2. `/docs/agent/13_VERIFICATION_GATE_PROTOCOL.md`
3. Current `PHASE_BRIEF.md`
4. All completed task reports for this phase

## Required checks

1. Confirm every phase task is complete, deferred, or blocked with explanation.
2. Compare changed files against each task's `allowed_paths`.
3. Confirm no skipped/focused tests were added.
4. Confirm no secrets are committed/logged.
5. Confirm no unapproved dependency/lockfile changes.
6. Confirm no unapproved destructive changes.
7. Run project verification commands in clean checkout if available.
8. Confirm R2 tasks have required review or logged waiver.
9. Confirm documentation/status files are updated.
10. Confirm user approval gates were respected.

## Acceptance criteria

- [ ] All checks have evidence.
- [ ] Failures are blocking or explicitly waived.
- [ ] No prose-only verification claims are accepted.
- [ ] Supervisor can make approve/fix/escalate decision.

## Reporting section

### Phase tasks reviewed

| Task | Status | Report present? | Notes |
|---|---|---:|---|
| [task] | Complete/Blocked | Yes/No | [notes] |

### Scope results

| File | Expected by task? | Authorized? | Notes |
|---|---:|---:|---|
| [file] | Yes/No | Yes/No | [notes] |

### Verification results

| Check | Command/method | Exit code | Result | Evidence excerpt |
|---|---|---:|---|---|
| [check] | `[command]` | [code] | Pass/Fail | [output] |

### Waivers

| Waiver | Approved by | Reason | Follow-up |
|---|---|---|---|
| [waiver] | [owner] | [reason] | [follow-up] |

### Recommendation

Approve / Launch fix task / Escalate / Wait for user input

## Next

- Current status:
- Waiting on:
- Next action:
- Owner:
