# Task: Audit and Classify Environment Variables

## Purpose

Create a complete inventory of current environment variables and classify them by environment, sensitivity, and runtime usage before staging/production separation.

## Required reading

Before execution, read:

1. `/docs/agent/03_SUBAGENT_EXECUTION_RULES.md`
2. `/docs/agent/04_QUALITY_BAR.md`
3. `/docs/agent/05_SECURITY_GUARDRAILS.md`
4. This task file fully, twice.
5. `PHASE_BRIEF.md` for this phase.

Do not read the full project overview unless explicitly instructed.

## Context summary

This task is part of foundation work for a consumer SaaS app. The project must separate local, staging, and production before adding user-facing auth, billing, and notifications.

## User inputs required

None for this task.

## Files/areas likely involved

- `.env.example`
- environment/config files
- hosting config files
- README/deployment docs
- source files that read `process.env`

## Files/areas forbidden

- Do not modify production secrets.
- Do not create hosting projects.
- Do not change deployment settings.
- Do not implement env validation in this task unless already present and required for inventory.

## Required implementation

1. Search the codebase for environment variable usage.
2. Create or update an environment inventory document.
3. For each env var, document:
   - name
   - where it is used
   - client/public or server-only
   - secret or non-secret
   - required in local/staging/production
   - provider/source
   - notes/risks
4. Identify any env vars that appear unsafe, ambiguous, duplicated, or missing from `.env.example`.
5. Do not rename variables in this task.
6. Do not add validation logic in this task.

## Non-goals

- Do not configure Vercel/hosting.
- Do not configure database provider.
- Do not change runtime behavior.
- Do not add new services.

## Security rules

- Do not print or commit actual secret values.
- Only document variable names and purpose.
- If a secret appears committed, stop and report immediately.

## Acceptance criteria

- [ ] All detected env vars are listed.
- [ ] Each env var has sensitivity classification.
- [ ] Each env var has local/staging/production requirement classification.
- [ ] Public/client env vars are distinguished from server-only env vars.
- [ ] Missing `.env.example` entries are listed.
- [ ] Risks are documented.

## Verification commands

Run:

```bash
pnpm typecheck
pnpm lint
```

If these commands do not exist, document why.

## Failure/stop conditions

Stop and report if:

- committed secrets are found
- env usage is too dynamic to classify safely
- running commands would require missing dependencies not covered by the task

## Reporting

### Files changed
-

### What was implemented
-

### Env vars classified
| Name | Runtime | Secret? | Local | Staging | Production | Notes |
|---|---|---:|---:|---:|---:|---|

### Verification results
| Command | Result | Notes |
|---|---|---|
| `pnpm typecheck` | | |
| `pnpm lint` | | |

### Known issues
-

### Follow-up tasks
-

### Commit
- Message: `foundation: audit environment variable usage`
- Hash, if available:
