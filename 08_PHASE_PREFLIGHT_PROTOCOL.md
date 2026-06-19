# 08. Phase Preflight Protocol

## Purpose

Before a phase begins, the Supervisor must confirm that required user inputs, accounts, keys, decisions, and data are available.

This prevents subagents from improvising around missing real-world setup.

## Core rule

```text
No phase starts until its preflight requirements are checked.
```

## Phase brief requirement

Every `PHASE_BRIEF.md` must include:

```md
## User Inputs Required Before Phase Starts
```

This section must list all required:

- accounts
- registrations
- keys/secrets
- URLs
- domains
- provider setup
- product decisions
- legal/compliance decisions
- sample data
- test accounts
- budget/plan approvals
- external access permissions

## Required format for each input

Each required input must include:

```md
### Input: [Exact name]

**Needed for:**
[Task or phase this unblocks]

**Why it is needed:**
[Specific reason]

**How to get it:**
1. [Step]
2. [Step]
3. [Step]

**Where to put/provide it:**
[.env, Vercel, Supabase, Stripe, uploaded file, decision comment, etc.]

**Safety warning:**
[What not to commit/share]

**Blocked until provided:**
- [Task file]

**Can continue without it:**
- [Task file]

**Next after provided:**
[Exactly what the supervisor/subagent will do next]
```

## Example: Supabase staging project

```md
### Input: Supabase staging project URL and anon key

**Needed for:**
Staging environment wiring and deployment verification.

**Why it is needed:**
The staging app must connect to an isolated staging database instead of production.

**How to get it:**
1. Open Supabase.
2. Create or select the staging project.
3. Go to Project Settings → API.
4. Copy `Project URL`.
5. Copy `anon public key`.

**Where to put/provide it:**
Add them to Vercel Staging environment variables as:
- `NEXT_PUBLIC_SUPABASE_URL`
- `NEXT_PUBLIC_SUPABASE_ANON_KEY`

**Safety warning:**
Do not commit these values to the repo. Do not use production Supabase values for staging.

**Blocked until provided:**
- `03_vercel-project-separation.md`
- `08_staging-production-verification.md`

**Can continue without it:**
- `01_environment-inventory.md`
- `02_environment-contract-and-validation.md`
- `07_deployment-docs.md`

**Next after provided:**
The supervisor will launch staging environment wiring and then run the staging deployment verification task.
```

## Supervisor preflight duties

Before launching tasks, the Supervisor must classify inputs:

```text
Available
Missing but not blocking
Missing and blocking
Requires user decision
Requires account registration
Requires secret/key
Requires production-risk approval
```

## Launch rule

The Supervisor may launch non-blocked tasks while waiting for user input.

Example:

```text
Env audit and docs can run now. Vercel wiring waits on staging project values.
```

## Do not fake inputs

Agents must not:

- invent API keys
- use production credentials as staging placeholders
- commit fake secrets that look real
- skip verification because credentials are missing
- silently use local-only config when task requires hosted staging

## User request quality

Every preflight request to the user must follow `04_COMMUNICATION_PROTOCOL.md`.

It must explain:

- what is needed
- why it is needed
- how to get it
- where to provide it
- safety warning
- what happens next

## Preflight report

Before phase execution, the Supervisor should produce:

```md
## Phase Preflight Report

### Ready inputs
-

### Missing non-blocking inputs
-

### Blocking inputs
-

### Tasks that can start now
-

### Tasks that must wait
-

### Recommended next action
-
```
