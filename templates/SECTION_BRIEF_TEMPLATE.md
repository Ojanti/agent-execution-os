# Section [Number]: [Section Name]

## Purpose

[Explain why this section exists.]

## Business goal

[Explain the business/product outcome.]

## Technical goal

[Explain the technical outcome.]

## What changes by the end of this section

- [Change]

## What must not change

- [Boundary]

## Known risks

| Risk | Severity | Mitigation |
|---|---|---|
| [Risk] | [Low/Med/High] | [Mitigation] |

## Relevant architecture areas

- [Area/file/system]

## Required standards

Supervisors and subagents must follow:

- `/docs/agent/04_QUALITY_BAR.md`
- `/docs/agent/05_SECURITY_GUARDRAILS.md`
- `/docs/agent/04_COMMUNICATION_PROTOCOL.md` if present in project pack

## Phase list

| Phase | Name | Status | Dependency |
|---:|---|---|---|
| 1 | [Phase] | Not started | None |

## Phase dependencies

[Explain important sequencing.]

## Supervisor responsibilities

The Supervisor for this section must:

- run phase preflight checks
- identify required user inputs
- sequence tasks
- parallelize safe independent tasks
- launch subagents using task files
- review subagent reports
- update section status
- escalate blockers

## Section-level done criteria

- [ ] All phases complete
- [ ] Verification gates passed
- [ ] Security guardrails satisfied
- [ ] Status files updated
- [ ] Director approval received

## Escalation conditions

Escalate to Director/user if:

- product scope changes
- missing input blocks progress
- security tradeoff appears
- production risk appears
- phase acceptance criteria cannot be met

## Next

- Current status:
- Waiting on:
- Next action:
- Owner:
