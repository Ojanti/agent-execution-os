# 04. Communication Protocol

## Purpose

This protocol prevents agents from creating vague, frustrating, or unusable messages.

Every communication must be useful, actionable, and clear about what happens next.

## Core rule

```text
Never ask the user for something without telling them exactly how to get it and what happens next.
```

## User Request Protocol

Any request made to the user must be specific, actionable, and self-contained.

When asking the user for anything, include:

1. **What is needed**
   - Name the exact account, key, file, URL, registration, decision, or data needed.

2. **Why it is needed**
   - Explain the specific task, phase, or blocker it affects.

3. **How the user can get it**
   - Give step-by-step instructions.
   - Include where to click, what page to open, what setting to copy, or what format to provide.
   - If there are multiple options, recommend the simplest one.

4. **Where/how to provide it**
   - Say whether it should be pasted into Cursor, added to `.env`, uploaded as a file, added in Vercel, added in Supabase, etc.
   - Never ask the user to paste secrets into chat unless explicitly approved by the user.

5. **Safety warning, when relevant**
   - For secrets, credentials, production access, billing, domains, or customer data, explain what must not be shared publicly or committed.

6. **What happens next**
   - End every user-facing message with a concise “Next” section explaining exactly what will happen after the user provides the item.

## Bad request

```text
Need Supabase keys.
```

## Good request

```text
I need the Supabase staging project URL and anon key so the staging environment can connect to the correct database.

How to get them:
1. Open Supabase.
2. Select the staging project.
3. Go to Project Settings → API.
4. Copy `Project URL` and `anon public key`.
5. Add them to Vercel Staging as `NEXT_PUBLIC_SUPABASE_URL` and `NEXT_PUBLIC_SUPABASE_ANON_KEY`.

Safety: do not commit these values to the repo. The anon key is public-ish, but it still belongs in environment configuration, not source code.

Next: once these are added, I will run the staging deployment verification task and confirm the app connects to staging Supabase.
```

## Communication footer rule

Every user-facing communication must say what happens next.

For detailed updates, use:

```md
## Next

- Current status:
- Waiting on:
- Next action:
- Owner:
```

For short updates, use:

```text
Next: waiting for the Supabase staging URL/key. After that, run staging deployment verification.
```

## Actor-specific communication rules

### Director

Director asks for:

- product decisions
- account registrations
- budget/plan choices
- launch decisions
- risk approvals
- cross-section tradeoffs

Director messages must include:

```text
Decision needed
Options
Recommendation
How to complete it
What happens next
```

### Supervisor

Supervisor asks for:

- phase prerequisites
- missing accounts/keys
- missing data
- approval to unblock sequencing
- confirmation of user-side setup

Supervisor messages must include:

```text
Input needed
How to get it
Which tasks are blocked
Which tasks can continue
What happens next
```

### Subagent

Subagent asks for:

- specific implementation blockers
- missing env values
- missing file contents
- clarification when task instructions conflict

Subagents must not ask vague strategy questions. They should escalate those to the Supervisor.

## Status update style

Status updates should be short unless a report is requested.

Good:

```text
Phase 1.1 is partially unblocked. Env inventory and documentation can run now; Vercel/Supabase wiring waits on staging project details.

Next: launch the parallel audit/doc tasks, then request staging credentials before environment wiring.
```

Bad:

```text
I will now begin working through everything and keep you posted.
```

## Reporting style

Reports must be structured and factual.

Do not bury failures.

A completion report must include:

- completed work
- files changed
- verification results
- known risks
- follow-ups
- whether the task is truly complete

## Safety communication

For sensitive data, always say:

- do not paste secrets into public chat
- do not commit secrets
- use environment variables or secret manager
- production values require extra care

## No vague blockers

Forbidden:

```text
Need credentials.
Need access.
Need more info.
Something is broken.
Tests failed.
```

Required:

```text
I need `STRIPE_WEBHOOK_SECRET` from Stripe test mode because webhook verification cannot be tested without it.
How to get it: Stripe Dashboard → Developers → Webhooks → select the local/staging endpoint → reveal Signing secret.
Add it to `.env.local` as `STRIPE_WEBHOOK_SECRET` and to Vercel Staging under Environment Variables.
Next: after it is added, rerun webhook verification tests.
```
