# 05. Quality Bar

## Purpose

The quality bar defines what “done” means.

A task is not complete because files were edited. A task is complete only when implementation, verification, reporting, and risk documentation are complete.

## How to use this file

This is a base quality bar. Every project must extend it.

Sections marked **CORE** must not be removed.
Sections marked **EXTEND** should be customized per project.
Sections marked **OPTIONAL** apply only when relevant.

## Universal Definition of Done — CORE

A task is done only when:

- implementation matches the task scope
- non-goals were respected
- no unrelated cleanup was performed
- required verification commands were run
- failures are documented honestly
- security guardrails were followed
- acceptance criteria are checked one by one
- a report section is filled in
- follow-up risks are listed
- commit message matches the requested format, if commit is requested

## Scope Quality — CORE

Agents must:

- do only the assigned task
- avoid “while I’m here” changes
- not refactor unrelated code
- not change product direction
- not invent architecture outside the task
- stop if instructions conflict

## Engineering Quality — EXTEND

Base standard:

- code should be simple, maintainable, and typed where possible
- avoid duplicated logic unless intentionally isolated
- avoid hidden side effects
- prefer explicit names over clever abstractions
- preserve existing conventions unless the task says to change them
- add comments only when they clarify non-obvious decisions

Extend this section with project-specific standards:

- language/framework conventions
- folder structure rules
- naming conventions
- API conventions
- state management conventions
- package manager commands
- formatting/lint rules

## TypeScript Quality — OPTIONAL

Apply for TypeScript projects.

Base standard:

- no unnecessary `any`
- no unsafe type assertions unless justified
- no ignored type errors without explanation
- exported functions/components should have understandable types
- env/config values should be validated before use
- external inputs should be parsed/validated before trusted

## Testing Expectations — EXTEND

Base standard:

- run the verification commands listed in the task file
- do not claim tests pass unless they were run
- if tests cannot run, explain exactly why
- document unrelated existing failures separately
- add tests when the task changes critical behavior

Extend per project:

- unit tests
- integration tests
- E2E tests
- visual regression
- accessibility tests
- migration tests
- API contract tests
- AI evaluation tests

## UX Expectations — EXTEND

Base standard:

Any user-facing change should handle relevant states:

- loading
- empty
- error
- success
- disabled/unavailable
- permission denied

User-facing copy should be clear, not vague.

Extend per project:

- design system usage
- responsive behavior
- mobile expectations
- accessibility standards
- onboarding UX
- empty states
- error tone
- internationalization/localization

## Accessibility Expectations — EXTEND

Base standard:

- interactive elements must be keyboard/focus accessible where relevant
- labels must be clear
- disabled states must be understandable
- color must not be the only indicator of meaning
- semantic structure should be preserved

Extend per project:

- WCAG target
- screen reader testing
- keyboard testing
- mobile accessibility
- design system a11y rules

## Security Expectations — CORE

Agents must:

- never commit secrets
- never log secrets
- never weaken auth to pass tests
- never expose private user data
- never bypass tenant isolation in user-facing code
- never trust client-side billing/subscription state as source of truth
- never add unauthenticated admin, cron, or webhook routes
- never remove validation to make code easier

More details live in `06_SECURITY_GUARDRAILS.md`.

## Database/Migration Expectations — OPTIONAL

Apply when the project uses a database.

Base standard:

- migrations should be safe and reversible when possible
- data ownership must be explicit
- indexes should match expected queries
- constraints should protect data integrity
- destructive changes require explicit approval
- seed data must not include real private user data unless explicitly approved

For multi-user apps:

- user/tenant ownership must be explicit
- RLS or equivalent isolation must be tested
- User A must not read User B’s data

## API Expectations — OPTIONAL

Base standard:

- validate inputs
- return clear errors
- protect private routes
- rate-limit abuse-prone routes where relevant
- avoid leaking internal errors to users
- do not expose service/admin credentials
- do not trust user-controlled URLs without SSRF protection

## AI/LLM Expectations — OPTIONAL

Apply to AI-powered projects.

Base standard:

- expensive model calls should be gated by quota/rate limits where relevant
- prompts should be versioned or documented if product-critical
- outputs should be validated before persistence when possible
- user data sent to providers should be intentional and documented
- fallback behavior should exist for provider failure
- never claim AI output is deterministic unless verified

Extend per project:

- model/provider choices
- cost budgets
- evaluation datasets
- prompt contracts
- privacy constraints
- retry/circuit-breaker rules

## Billing Expectations — OPTIONAL

Apply when payments/subscriptions exist.

Base standard:

- billing source of truth must be server-side/webhook-driven
- never trust client-only plan state
- verify webhooks
- handle failed payments
- handle cancellation/downgrade
- avoid exposing billing secrets
- test in sandbox/test mode before live mode

## Documentation Expectations — CORE

Every task report must document:

- files changed
- what was implemented
- verification results
- known issues
- follow-up tasks
- commit message/hash if applicable

## Stop Conditions — CORE

Stop and report when:

- required user input is missing
- task instructions conflict
- security would need to be weakened
- destructive migration is needed but not approved
- production data might be affected
- scope must expand beyond the task
- verification fails in a way that cannot be safely resolved in scope

## Project-Specific Extensions

Add project-specific quality rules below when adapting this system.

```text
Project type:
Risk level:
Required verification commands:
Required UX states:
Accessibility target:
Security extensions:
Testing extensions:
AI/cost extensions:
Deployment requirements:
```

## v1.1 Truth Layer Requirements — CORE

Every executable task must include risk metadata, `allowed_paths`, approval flags, verification commands, and stop conditions.

A task is not done unless verification evidence includes command output and exit codes or a clear explanation for why verification could not run.

Supervisors must not accept prose-only “passed” claims.

R2 and phase gates require stricter verification and clean-checkout checks where available.
