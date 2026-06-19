# 09. Parallelization Protocol

## Purpose

This protocol helps Supervisors decide which tasks can run in parallel and which must run sequentially.

Parallel execution saves time, but unsafe parallelization creates conflicts and rework.

## Core rule

```text
Parallelize independent work. Sequence shared contracts, migrations, auth/security boundaries, and verification gates.
```

## Supervisor responsibility

For every phase, the Supervisor must classify tasks as:

```text
Can run immediately
Can run in parallel
Blocked by user input
Blocked by another task
Must run sequentially
Verification gate
```

## Tasks can run in parallel when

- they touch separate file areas
- they do not depend on each other’s output
- they do not define shared contracts
- they do not create competing migrations
- they do not modify the same central config files
- they do not both change auth/security logic
- each has independent verification

## Tasks must run sequentially when

- one task creates schema another consumes
- one task defines env variables another uses
- one task changes auth boundaries another must respect
- one task creates a design/API contract another implements
- both tasks touch the same central file
- both tasks create migrations
- one task produces decisions needed by another
- one task must verify the outputs of previous tasks

## Verification gates

Verification gates always run after implementation tasks.

They must not run in parallel with tasks they are verifying.

## Phase brief dependency map

Every `PHASE_BRIEF.md` should include:

```md
## Task Dependency Map

### Can start immediately
- `01_task-a.md`
- `02_task-b.md`

### Can run in parallel after Task 01
- `03_task-c.md`
- `04_task-d.md`

### Must wait until implementation tasks complete
- `08_phase-verification-gate.md`

### Blocked by user input
- `05_task-e.md` requires [input]
```

## Example: staging/production phase

```text
Task 01: Environment inventory
Can start immediately.

Task 02: Environment contract and validation
Depends on Task 01.

Task 03: Vercel project separation
Depends on Task 02 and Vercel access/user input.

Task 04: Supabase project separation
Can run after Task 01, but actual wiring needs Supabase staging details.

Task 05: Seed data and test accounts
Depends on Supabase staging project existing.

Task 06: Cron/worker environment safety
Depends on Task 02.

Task 07: Deployment docs
Can run after Task 02, parallel with Task 03/04.

Task 08: Verification gate
Runs last.
```

## Conflict indicators

Do not parallelize if tasks both touch:

- env validation file
- central database schema
- migration order
- route middleware
- auth provider setup
- package manager files
- global config
- shared component API
- billing provider setup

## Supervisor launch format

When launching parallel tasks, the Supervisor should use one message with multiple task calls if the tool supports it.

Prompt should be minimal:

```text
Read `[task path]` and execute every instruction. Follow verification steps. Fill in the Reporting section. Commit with the specified message.
```

## After parallel tasks complete

The Supervisor should:

1. Read completion summaries.
2. Identify conflicts or failures.
3. Launch fix tasks if needed.
4. Only then launch dependent tasks.
5. Update phase status.

## Stop condition

If parallel tasks produce conflicting changes, stop sequencing and report:

- which tasks conflicted
- files involved
- safest resolution path
- whether user/Director decision is needed
- what happens next
