# Phase 1.1: Staging/Production Separation

## Phase goal

Create a safe local → staging → production environment model so future auth, billing, notification, and user-data work can be tested before production.

## Why this phase exists

Consumer SaaS work becomes dangerous without environment separation. Staging must use isolated services and test credentials so production data, billing, and users are protected.

## Prerequisites

- Repo is accessible locally.
- Package manager command is known.
- Hosting provider access exists or can be requested.
- Database provider access exists or can be requested.

## User Inputs Required Before Phase Starts

### Input: Hosting staging project or environment

**Needed for:**
Hosted staging deployment.

**Why it is needed:**
The app needs a hosted staging environment that is separate from production.

**How to get it:**
1. Open the hosting provider dashboard.
2. Create a new staging project or enable preview/staging environment.
3. Connect it to the repository/branch used for staging.
4. Open Environment Variables for the staging environment.

**Where to put/provide it:**
Provide the staging project URL and confirm where staging env vars should be added.

**Safety warning:**
Do not copy production secrets into staging unless explicitly approved. Use test-mode provider keys where possible.

**Blocked until provided:**
- `03_hosting-project-separation.md`
- `08_phase-verification-gate.md`

**Can continue without it:**
- `01_environment-inventory.md`
- `02_environment-contract-and-validation.md`
- `07_deployment-docs.md`

**Next after provided:**
The supervisor will launch hosting environment wiring and deployment verification.

## Task list

| Task | File | Status |
|---:|---|---|
| 1 | `01_environment-inventory.md` | Not started |
| 2 | `02_environment-contract-and-validation.md` | Not started |
| 3 | `03_hosting-project-separation.md` | Not started |
| 4 | `04_database-project-separation.md` | Not started |
| 5 | `05_seed-data-and-test-accounts.md` | Not started |
| 6 | `06_cron-worker-environment-safety.md` | Not started |
| 7 | `07_deployment-docs.md` | Not started |
| 8 | `08_phase-verification-gate.md` | Not started |

## Task Dependency Map

### Can start immediately
- `01_environment-inventory.md`

### Depends on Task 01
- `02_environment-contract-and-validation.md`

### Can run after Task 02
- `06_cron-worker-environment-safety.md`
- `07_deployment-docs.md`

### Blocked by user input
- `03_hosting-project-separation.md`
- `04_database-project-separation.md`
- `05_seed-data-and-test-accounts.md`

### Verification gate
- `08_phase-verification-gate.md`

## Phase acceptance criteria

- [ ] Local/staging/production environment responsibilities are documented.
- [ ] Required env variables are classified.
- [ ] Staging does not point to production services.
- [ ] Secrets are not committed.
- [ ] Verification commands pass or failures are documented.
- [ ] Deployment docs explain how to configure staging and production.
