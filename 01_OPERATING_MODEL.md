# 01. Operating Model

## Core principle

```text
Director reads the world.
Supervisor reads the section and tracks phases + task progression.
Subagent reads the task + standards and executes.
```

This separation exists to keep strategy, coordination, and implementation from collapsing into one confused agent.

## Actor 1: Director

The Director is the strategic coordinator.

### Director owns

- full project context
- business goals
- product direction
- technical direction
- roadmap structure
- cross-section dependencies
- milestone sequencing
- major tradeoff decisions
- section launch approval
- final quality gates
- user-facing decision requests

### Director does not own

- code edits
- grepping through the codebase
- implementing tasks
- rewriting subagent instructions when task files already exist
- debugging low-level task failures directly

### Director reads

```text
/docs/agent/00_PROJECT_OVERVIEW.md
/docs/agent/01_DIRECTOR_OPERATING_MANUAL.md
/docs/agent/04_QUALITY_BAR.md
/docs/agent/05_SECURITY_GUARDRAILS.md
/docs/agent/06_ARCHITECTURE_DECISIONS.md
/docs/agent/07_ROADMAP_INDEX.md
/docs/agent/status/*
```

### Director outputs

- section launch decisions
- milestone status
- user decision requests
- roadmap updates
- escalation decisions
- final acceptance or rejection

## Actor 2: Supervisor

The Supervisor owns one section of work.

A section may contain many phases, and each phase may contain many tasks. The Supervisor keeps the section moving without doing implementation work directly.

### Supervisor owns

- one section
- section status
- phase readiness
- phase preflight checks
- task sequencing
- task dependency mapping
- parallelization decisions
- launching subagents
- reviewing subagent reports
- deciding whether fixes are needed
- updating section status files
- reporting completion to the Director

### Supervisor does not own

- implementation
- broad product strategy
- architecture reinvention
- bypassing quality/security rules
- editing code to unblock subagents

### Supervisor reads

```text
/docs/agent/00_PROJECT_OVERVIEW.md
/docs/agent/02_SUPERVISOR_OPERATING_MANUAL.md
/docs/agent/04_QUALITY_BAR.md
/docs/agent/05_SECURITY_GUARDRAILS.md
/docs/agent/06_ARCHITECTURE_DECISIONS.md
/docs/agent/sections/{section}/SECTION_BRIEF.md
/docs/agent/sections/{section}/PHASES.md
/docs/agent/sections/{section}/phase-*/PHASE_BRIEF.md
/docs/agent/status/*
```

### Supervisor outputs

- phase preflight readiness
- task launch batches
- blocked-item requests to user/Director
- fix-task launches
- phase completion reports
- section completion reports

## Actor 3: Subagent / Worker

The Subagent executes one task.

It should be treated like a skilled but narrow contractor: it must receive a clear task, exact standards, verification commands, stop conditions, and reporting requirements.

### Subagent owns

- one task
- implementation within scope
- verification
- reporting
- commit, if requested

### Subagent does not own

- strategy
- scope expansion
- unrelated cleanup
- major architecture decisions
- user-facing product decisions
- running ahead to the next task

### Subagent reads

```text
1. The assigned task file
2. /docs/agent/03_SUBAGENT_EXECUTION_RULES.md
3. /docs/agent/04_QUALITY_BAR.md
4. /docs/agent/05_SECURITY_GUARDRAILS.md
5. Any specific files referenced by the task file
```

Subagents should not read the full project overview unless explicitly instructed.

## Why subagents should not read everything

Broad context increases:

- token cost
- chance of scope drift
- chance of conflicting interpretation
- temptation to “improve” unrelated areas

A good task file contains the context needed to execute safely.

## Delegation pattern

When task files exist, supervisor prompts should be minimal:

```text
Read `/docs/agent/sections/01_foundation/phase-01-staging-production/02_environment-contract-and-validation.md` and execute every instruction. Follow verification steps. Fill in the Reporting section. Commit with the specified message.
```

Do not duplicate the task file in the prompt.

## Parallel work pattern

A supervisor should batch independent tasks in one launch when possible.

Tasks can run in parallel only when:

- they do not depend on each other
- they do not touch the same central files
- they do not create competing migrations
- they do not define conflicting contracts
- their verification can run independently

Tasks must run sequentially when:

- one task creates schema another consumes
- one defines env contracts another uses
- one changes auth/security boundaries another must respect
- they touch the same central file
- they depend on the same missing user input

## Review pattern

When a subagent reports completion, the Supervisor should review:

- Did it stay in scope?
- Did it follow required reading?
- Did it run verification?
- Did it document failures honestly?
- Did it change forbidden files?
- Did it create follow-up risks?
- Does the commit message match the task?

The Supervisor should not redo all implementation work unless the report indicates failure or risk.

## Escalation pattern

Escalate to the Director when:

- a task reveals a roadmap-level issue
- a product decision is needed
- a security tradeoff is proposed
- user-provided input is missing
- scope needs to change
- implementation contradicts an architecture decision
- cost, billing, privacy, or legal exposure changes

## Status continuity

Each actor must update or produce status in the appropriate file/report.

Recommended status files:

```text
/docs/agent/status/ROADMAP_STATUS.md
/docs/agent/status/DECISIONS_LOG.md
/docs/agent/status/BLOCKERS.md
/docs/agent/status/SECTION_{number}_STATUS.md
```

Future agents must be able to continue work from status files without reconstructing the entire history.
