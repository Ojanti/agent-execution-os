# 03. Document Creation Protocol

## Purpose

This protocol defines how Agent Execution OS documents must be created.

A weak document creates weak agent behavior. The quality of execution depends directly on the quality of the section, phase, and task files.

## Golden rule

```text
The operating system is stable.
The project pack is custom.
The quality bar is inherited, then extended.
The task file is the source of truth for execution.
```

## Required creation sequence

For a new project, create documents in this order:

1. Project Overview
2. Architecture Decisions
3. Quality Bar extension
4. Security Guardrails extension
5. Roadmap Index
6. Section Briefs
7. Phase Briefs for the first section
8. Task execution files for the first phase
9. Status files
10. Director/Supervisor/Subagent manuals adapted to the project

## Project Overview requirements

`00_PROJECT_OVERVIEW.md` must include:

- project name
- project type
- business goal
- technical goal
- current state
- target state
- what the product is
- what the product is not
- current architecture
- known risks
- key decisions already made
- coding standards
- testing standards
- security expectations
- UX expectations
- data/privacy expectations
- deployment/environments
- AI/cost expectations, if relevant
- how to use the document set
- actor model

## Section Brief requirements

Each `SECTION_BRIEF.md` must include:

```text
Purpose
Business goal
Technical goal
What changes by end of section
What must not change
Known risks
Relevant architecture areas
Required standards
Phase list
Phase dependencies
Section-level done criteria
Supervisor responsibilities
Escalation conditions
```

## Phase Brief requirements

Each `PHASE_BRIEF.md` must include:

```text
Phase goal
Why this phase exists
Prerequisites
User inputs required before phase starts
Task list
Dependency map
Parallelization plan
Shared files/areas likely touched
Forbidden changes
Risk areas
Security concerns
Phase acceptance criteria
Phase verification gate
Supervisor reporting template
```

## Task Execution File requirements

Every task file must include:

```text
Purpose
Required reading
Context summary
User inputs required, if any
Files/areas likely involved
Files/areas forbidden
Step-by-step implementation instructions
Non-goals
Security rules
Data/model rules
UX rules, if relevant
Testing requirements
Acceptance criteria
Verification commands
Failure/stop conditions
Reporting section
Commit message
```

## Required reading block for every task

Every task file must include this block or a project-specific equivalent:

```md
## Required reading

Before execution, read:

1. `/docs/agent/03_SUBAGENT_EXECUTION_RULES.md`
2. `/docs/agent/04_QUALITY_BAR.md`
3. `/docs/agent/05_SECURITY_GUARDRAILS.md`
4. This task file fully, twice.

If this task references a `PHASE_BRIEF.md`, read that too.

Do not read the full project overview unless explicitly instructed.
```

## What “thorough” means

A task is thorough when a competent but project-unfamiliar agent can execute without guessing.

It must answer:

- What exactly am I changing?
- Why am I changing it?
- What files are likely involved?
- What files must I avoid?
- What is out of scope?
- What should I verify?
- What should I do if verification fails?
- What must I report?
- What commit message should I use?

## Bad vs good examples

### Bad

```text
Implement staging and production.
```

### Better

```text
Create separate staging and production environment configuration.
```

### Excellent

```text
Audit all current environment variables, classify each as local/staging/production/shared, create a typed env contract, update `.env.example`, add fail-fast validation for required server/client env values, and document which values must be configured in Vercel staging vs production. Do not create new Vercel projects in this task. Do not change runtime behavior except env loading/validation. Verify with typecheck, lint, and build.
```

## Task split rule

Split a task when it:

- touches more than one major subsystem
- requires separate verification modes
- mixes audit and implementation and deployment
- needs user input halfway through
- cannot be reverted independently
- has unclear ownership
- creates a migration plus UI plus API changes
- changes auth and data model together

## User input rule

Any file that asks the user for something must include:

- what is needed
- why it is needed
- how to get it, step by step
- where to put/provide it
- safety warning, if relevant
- what happens next

Never ask vague questions.

## Documentation status

Each section should classify documentation depth:

```text
FULLY DETAILED: ready for subagent execution
MEDIUM DETAIL: phase-level planning exists, tasks not fully written
OUTLINE ONLY: future area, not ready for execution
```

## Creation acceptance criteria

Before a phase starts, the Supervisor must confirm:

- phase brief exists
- user inputs are listed
- task files exist for all tasks to launch
- tasks have acceptance criteria
- tasks have verification commands
- tasks have stop conditions
- tasks have report sections
- dependencies/parallelization are explicit
- quality/security files are referenced
