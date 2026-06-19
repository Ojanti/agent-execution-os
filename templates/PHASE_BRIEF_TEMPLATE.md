# Phase [Number]: [Phase Name]

## Phase goal

[Explain what must be true when this phase is complete.]

## Why this phase exists

[Explain business/product/technical reason.]

## Prerequisites

- [Prerequisite]

## User Inputs Required Before Phase Starts

The Supervisor must confirm each item before launching dependent tasks.

For every item, include what is needed, why, how to get it, where to provide it, safety warning, and what happens next.

| Input | Required? | Blocks | How user gets it | Where to provide it | Safety warning |
|---|---:|---|---|---|---|
| [Input] | Yes/No | [Task/phase] | [Steps] | [Location] | [Warning] |

## Risk profile

| Area | Risk class | Reason | Extra gate? |
|---|---|---|---:|
| [Area] | R0/R1/R2 | [Reason] | Yes/No |

## Task list

| Task | Risk | Status | Depends on | Can run parallel? |
|---|---|---|---|---:|
| `01_task.md` | R0/R1/R2 | Not started | None | Yes/No |

## Dependency map

### Can run immediately

- [Task]

### Can run in parallel after [Task]

- [Task]

### Must be sequential

- [Task]

### Blocked by user input

- [Task]

### Verification gate

- `NN_phase-verification-gate.md`

## Shared files/areas likely touched

- [File/area]

## Security concerns

- [Concern]

## Phase acceptance criteria

- [ ] [Criterion]

## Phase verification gate requirements

The phase verification gate must check:

- [ ] all task reports exist
- [ ] changed files are expected
- [ ] no edits outside allowed paths remain unexplained/unauthorized
- [ ] no skipped/focused tests were introduced
- [ ] no secrets were committed/logged
- [ ] no unapproved dependency changes
- [ ] no unapproved destructive changes
- [ ] verification commands passed or failures are documented
- [ ] R2 requirements satisfied or waived with logged reason
- [ ] status files updated

## Supervisor reporting template

At phase end, report:

- tasks completed
- tasks blocked/deferred
- user inputs still needed
- verification evidence
- risks and waivers
- recommendation: approve / fix / escalate

## Next

- Current status:
- Waiting on:
- Next action:
- Owner:
