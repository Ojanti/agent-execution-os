# 10. Reporting and Status Protocol

## Purpose

Status files and reports preserve continuity across agents and sessions.

Without reports, future agents waste tokens rediscovering what happened.

## Core rule

```text
If work changes the project state, the report/status must say what changed, what was verified, what is blocked, and what happens next.
```

## Subagent task report

Every task file must include a reporting section like this:

```md
## Reporting

Fill this before completion.

### Files changed
-

### What was implemented
-

### Acceptance criteria results
- [ ] Criterion 1
- [ ] Criterion 2

### Verification results
| Command | Result | Notes |
|---|---|---|
| `pnpm typecheck` | | |
| `pnpm lint` | | |
| `pnpm test` | | |

### Known issues
-

### Follow-up tasks
-

### Scope notes
-

### Commit
- Message:
- Hash, if available:
```

## Supervisor phase report

At the end of each phase, the Supervisor must report:

```md
# Phase Completion Report

## Phase

## Status
Complete / Blocked / Partially complete

## Tasks completed
-

## Tasks blocked
-

## User inputs still needed
-

## Verification gate result
-

## Risks
-

## Follow-up tasks
-

## Recommendation
Approve phase / fix issues / escalate to Director

## Next
-
```

## Director milestone report

At major milestones, the Director reports:

```md
# Milestone Report

## Milestone

## Current status

## Sections completed

## Sections in progress

## Blockers

## Key decisions made

## Risks

## Recommended next milestone

## User decisions needed

## Next
```

## Status files

Recommended files:

```text
/docs/agent/status/ROADMAP_STATUS.md
/docs/agent/status/DECISIONS_LOG.md
/docs/agent/status/BLOCKERS.md
/docs/agent/status/SECTION_01_STATUS.md
```

## ROADMAP_STATUS.md

Tracks:

- section status
- phase status
- current milestone
- blocked work
- next recommended action

## DECISIONS_LOG.md

Tracks decisions in this format:

```md
## DEC-001: [Decision title]

**Date:** YYYY-MM-DD
**Owner:** Director / User / Supervisor
**Decision:**
**Reason:**
**Alternatives considered:**
**Impact:**
**Follow-up:**
```

## BLOCKERS.md

Tracks blockers in this format:

```md
## BLK-001: [Blocker title]

**Status:** Open / Resolved
**Blocks:**
**Owner:** User / Director / Supervisor / External
**What is needed:**
**How to get it:**
**Safety warning:**
**Next after resolved:**
```

## Good report qualities

Good reports are:

- specific
- factual
- short enough to scan
- honest about failures
- clear about next steps
- tied to acceptance criteria

## Bad report examples

```text
Done.
```

```text
Implemented everything and fixed some issues.
```

```text
Tests mostly work.
```

## Good report example

```md
## Status
Task complete.

## Files changed
- `src/lib/env.ts`
- `.env.example`
- `docs/deployment.md`

## Implemented
- Added Zod-based env validation.
- Split server-only and public env access.
- Updated `.env.example` with staging/production notes.

## Verification
- `pnpm typecheck`: pass
- `pnpm lint`: pass
- `pnpm build`: pass

## Risks
- Production env values still need to be configured in Vercel.

## Next
Supervisor can launch Vercel staging wiring once the user provides staging project settings.
```
