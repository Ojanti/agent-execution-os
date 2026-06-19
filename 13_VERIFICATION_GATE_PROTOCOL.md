# 13. Verification Gate Protocol

## Purpose

Agent reports are not enough. Verification must produce evidence.

This protocol moves trust from agent self-reporting to deterministic checks: command output, exit codes, scope diff, secret scans, migration checks, and phase-level gates.

## Core rule

```text
No prose-only “passed”. Every verification claim needs evidence.
```

A worker may not report:

```text
Tests passed.
```

A worker must report:

```text
Command: pnpm test
Exit code: 0
Relevant output:
...
```

## Evidence-backed verification

Each task report must include a verification table:

| Check | Command / method | Exit code | Result | Evidence location / excerpt |
|---|---|---:|---|---|
| Typecheck | `pnpm typecheck` | 0 | Pass | [excerpt] |
| Lint | `pnpm lint` | 1 | Fail | [error excerpt] |

If a command cannot run, the worker must explain:

- why it could not run
- whether this is blocking
- what would be needed to run it
- what happens next

## Standard checks

Project packs must define exact commands. Base checks usually include:

```bash
pnpm lint
pnpm typecheck
pnpm test
pnpm build
```

For database work:

```bash
# project-specific examples only
supabase db reset
pnpm db:migrate
pnpm test:db
```

For security-sensitive work:

```bash
# examples only; adapt per project
secret scan
scope allowlist check
skipped/focused test check
lockfile diff check
migration safety check
```

## Scope verification

A task must verify changed files are inside `allowed_paths`.

Supervisor must reject a task report if:

- files changed outside `allowed_paths`
- the worker does not explain the exception
- the worker proceeded without approval after discovering the need

## Dependency and lockfile verification

If `approved_dependency_change: false`, the artifact must not include:

- package manifest changes
- lockfile changes
- dependency manager changes
- dependency version pinning changes

If a dependency change is required, the worker stops and asks for approval through the User Request Protocol.

## Destructive verification

If `approved_destructive: false`, the artifact must not include:

- destructive migrations
- data deletion scripts
- production reset scripts
- permanent customer/user data removal
- irreversible migration operations

If destructive work is required, stop and request explicit approval.

## Skipped or focused test checks

Workers must not add or leave behind:

- `.only`
- `.skip`
- focused test flags
- commented-out failing tests
- disabled assertions
- weakened auth/validation checks

A green build obtained by weakening checks is a failure.

## Clean-checkout verification

Required for:

- R2 tasks
- phase verification gates
- production/security-sensitive work
- any task where local cached state may hide failure

Clean-checkout verification means:

1. fresh clone or fresh worktree
2. fresh dependency install
3. fresh env setup using documented safe env values
4. run declared verification commands
5. record raw output and exit codes

If this cannot be done in the current tool environment, the report must say so and mark it as a risk.

## Phase verification gate

Every phase should end with a dedicated gate task, usually named:

```text
NN_phase-verification-gate.md
```

The gate checks the combined output of all phase tasks.

It must verify:

- all phase tasks completed or explicitly deferred
- all task reports exist
- all changed files are expected
- no cross-task conflicts remain
- typecheck/lint/test/build status
- no skipped/focused tests
- no secret leaks
- no unapproved dependency changes
- no unapproved destructive changes
- R2 requirements satisfied
- documentation/status files updated
- user-facing decisions approved where required

## Gate semantics

```text
Gates block artifacts, not operators.
Cost ledgers inform, they do not block.
```

A failed verification gate stops that artifact from being accepted. The Director/operator may still choose to fix, waive with explanation, or re-scope.

## Waivers

Waivers are allowed only when explicit and logged.

A waiver must include:

- what is being waived
- why it is safe or necessary
- who approved it
- affected task/phase
- expiry/follow-up, if any

R2 waivers should be rare.

## Supervisor acceptance rule

A Supervisor may not accept a task or phase based only on a completion summary.

The report must include:

- scope evidence
- verification evidence
- acceptance criteria status
- risk/follow-up notes

If evidence is missing, launch a fix/report-completion task or reject acceptance.
