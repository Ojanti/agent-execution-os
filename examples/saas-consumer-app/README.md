# Example: SaaS Consumer App

This example shows how Agent Execution OS can be adapted for a consumer SaaS product.

## Project type

Consumer SaaS with auth, billing, private user data, notifications, and onboarding.

## Risk profile

High, because it may involve:

- user accounts
- private user data
- billing
- third-party integrations
- email/push notifications
- production infrastructure

## Example sections

```text
Section 1: Foundation, Environments, Auth & Security
Section 2: Consumer Data Model & User Inbox
Section 3: User Profile, Preferences & Onboarding
Section 4: Source/Content Management & Personalization
Section 5: Delivery Intelligence & Notification Channels
Section 6: PWA/Mobile Web Experience
Section 7: Billing, Quotas & Usage Metering
Section 8: Support, Feedback & Observability
Section 9: Extension/External Capture, if relevant
Section 10: Launch Readiness & Growth Loops
```

## Example Section 1 phases

```text
Phase 1.1: Staging/production separation
Phase 1.2: Environment contract and secret boundaries
Phase 1.3: Auth and user identity
Phase 1.4: Tenant/user-scoped data model
Phase 1.5: RLS or equivalent authorization
Phase 1.6: API route, cron, and webhook hardening
Phase 1.7: Foundation verification gate
```

## Example phase: Staging/production separation

### Tasks

```text
01_environment-inventory.md
02_environment-contract-and-validation.md
03_hosting-project-separation.md
04_database-project-separation.md
05_seed-data-and-test-accounts.md
06_cron-worker-environment-safety.md
07_deployment-docs.md
08_phase-verification-gate.md
```

## Example user input request

```text
I need the staging database project URL and public client key so the staging app can connect to an isolated staging database instead of production.

How to get it:
1. Open your database provider dashboard.
2. Select the staging project.
3. Open API/settings.
4. Copy the project URL and public client key.
5. Add them to the hosting provider’s Staging environment variables.

Safety: do not use production database values for staging. Do not commit these values to the repo.

Next: once these are added, the staging deployment verification task can confirm the hosted app connects to the staging database.
```

## SaaS-specific quality extensions

- User-owned data must be scoped by authenticated user or tenant.
- Billing state must come from server/provider webhook state.
- Private routes must require auth.
- Webhooks must verify signatures.
- Admin/cron routes must require secrets or platform-level protection.
- Staging must not point to production database.
- Production data must not be used in seed scripts.
