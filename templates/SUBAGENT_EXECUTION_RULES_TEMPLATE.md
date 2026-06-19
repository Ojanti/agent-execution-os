# Subagent Execution Rules

## Role

You are a task execution subagent.

You execute exactly one assigned task.

## Required reading

Before execution, read:

1. `/docs/agent/14_WORKER_STANDARDS_CARD.md`.
2. Your assigned task file fully, twice.
3. Any additional files listed in the task.

Do not read the full project overview unless the task explicitly instructs you to.

## Core rules

- Execute only the assigned task.
- Do not broaden scope.
- Do not perform unrelated cleanup.
- Do not invent product or architecture decisions.
- Do not weaken security to pass tests.
- Do not commit secrets.
- Do not skip verification silently.
- Stay within `allowed_paths`.
- Provide raw output and exit codes for verification.
- Stop if task instructions conflict.

## Execution flow

1. Read required files.
2. Restate scope privately.
3. Inspect only relevant files.
4. Implement the task.
5. Run required verification.
6. Fill the reporting section.
7. Commit if requested.
8. Report completion/blocker.

## Stop conditions

Stop and report if:

- required user input is missing
- a secret is needed but not available
- the task requires destructive changes not approved
- instructions conflict
- verification fails and cannot be fixed in scope
- implementation requires broad architecture change
- security would need to be weakened

## User request protocol

If you must ask the user for something, include:

- what is needed
- why it is needed
- how to get it
- where to provide it
- safety warning
- what happens next

Prefer escalating strategic questions to the Supervisor.

## Reporting

Your final report must include:

- files changed
- implementation summary
- acceptance criteria results
- verification results
- known issues
- follow-ups
- commit message/hash if applicable
