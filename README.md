# Agent Execution OS

Agent Execution OS, or AEOS, is a reusable markdown-first operating system for coordinating AI agents through complex software and product work.

It helps you turn a large project into a structured execution system where one high-context Director coordinates section Supervisors, and Supervisors delegate tightly scoped work to cheaper Subagents or workers.

AEOS is not a coding framework. It is an execution framework.

## The core idea

```text
Director reads the world.
Supervisor reads the section and tracks phases + task progression.
Subagent reads the task + standards and executes.
```

This separation prevents one agent from trying to hold strategy, planning, implementation, verification, and status tracking all at once.

## What problem AEOS solves

AI agents are useful, but they often fail in predictable ways:

- they drift outside scope
- they edit unrelated files
- they over-trust their own summaries
- they say tests passed without evidence
- they ask the user vague questions
- they forget prior decisions
- they mix strategy and implementation
- they run expensive/high-risk work without enough gates
- parallel agents conflict with each other

AEOS reduces those failure modes by forcing work through:

- clear roles
- section/phase/task hierarchy
- task readiness checks
- risk classes
- path allowlists
- evidence-backed verification
- phase gates
- user-request rules
- status files
- Director-controlled sequencing

## When to use AEOS

Use AEOS when:

- the work spans multiple phases or files
- several AI agents may be used
- you need a repeatable execution plan
- quality, security, privacy, or cost drift would hurt
- you want cheaper subagents to execute safely
- user inputs, accounts, keys, or approvals may block phases
- you want future agents to continue from documented state

Do not use AEOS for tiny one-off edits where the process overhead is larger than the task.

## Actor model

### Director

The Director owns the whole project context.

It decides what section should run next, reviews Supervisor summaries, handles major tradeoffs, keeps roadmap status coherent, and gives the user exact prompts for starting new Supervisor sessions.

The Director does not implement code.

### Supervisor

A Supervisor owns one section of work.

It reads the section brief, tracks phases, checks preflight requirements, decides what can run in parallel, launches Subagents using task files, reviews reports, launches fix tasks, and sends phase/section summaries back to the Director.

The Supervisor does not implement code.

### Subagent / Worker

A Subagent executes one task.

It reads the assigned task file plus required standards, stays within `allowed_paths`, runs verification, reports evidence, and stops when the task requires approval or scope changes.

The Subagent does not own strategy.

## How the workflow runs

```text
1. AEOS is adapted into a project-specific /docs/agent pack.
2. The Director session starts from the project overview and roadmap.
3. The Director gives the exact prompt for launching a Supervisor.
4. The Supervisor reads the section docs and checks phase preflight.
5. The Supervisor launches Subagents for executable task files.
6. Subagents execute, verify, report, and commit if instructed.
7. The Supervisor reviews reports and runs phase gates.
8. The user pastes Supervisor milestone summaries back to the Director.
9. The Director decides the next move and provides the next Supervisor prompt.
```

You should not paste every worker report to the Director. The Supervisor handles task-level noise. Send the Director only phase completions, blockers, failed gates, section completions, major decisions, and R2/high-risk escalations.

## Quick start: adapt AEOS to a project

### Step 1: Put AEOS where an agent can read it

Use this repository as the reusable source framework.

For a real project, create a project-specific pack under:

```text
/docs/agent/
```

Do not work directly inside the AEOS repo unless you are improving AEOS itself.

### Step 2: Ask an AI agent to adapt AEOS

Give an AI agent access to your project and use this prompt:

```text
I want to adapt Agent Execution OS to this project.

Read the AEOS docs, especially:
- README.md
- 01_OPERATING_MODEL.md
- 02_DOCUMENT_SYSTEM.md
- 03_DOCUMENT_CREATION_PROTOCOL.md
- 04_COMMUNICATION_PROTOCOL.md
- 05_QUALITY_BAR.md
- 06_SECURITY_GUARDRAILS.md
- 07_TASK_GRANULARITY_RULES.md
- 08_PHASE_PREFLIGHT_PROTOCOL.md
- 09_PARALLELIZATION_PROTOCOL.md
- 10_REPORTING_AND_STATUS_PROTOCOL.md
- 11_ADAPTATION_AND_EXTENSION_GUIDE.md
- 12_RISK_CLASS_AND_ROUTING.md
- 13_VERIFICATION_GATE_PROTOCOL.md
- 14_WORKER_STANDARDS_CARD.md
- 15_TASK_FILE_READINESS_RUBRIC.md
- templates/*

Then inspect this project and create a project-specific /docs/agent pack.

Do not implement product code yet.

First, propose the section and phase breakdown for approval.

After approval, generate:
1. project overview
2. director operating manual
3. supervisor operating manual
4. subagent execution rules
5. roadmap index
6. architecture decisions file
7. status files
8. section briefs
9. phase briefs
10. fully detailed execution task files for the first section only
11. medium-detail outlines for later sections

Every task file must include risk_class, allowed_paths, acceptance criteria, verification commands, stop conditions, and reporting requirements.
```

### Step 3: Approve the section/phase breakdown

Before task files are written, review the proposed structure.

Make sure the plan uses this hierarchy:

```text
Section -> Phase -> Task
```

A Section is a major work pillar.
A Phase is a milestone within that pillar.
A Task is one executable unit for one worker.

### Step 4: Start the Director session

Open a dedicated Director session and use a prompt like:

```text
You are the Director for this project.

Read:
1. /docs/agent/00_PROJECT_OVERVIEW.md
2. /docs/agent/01_DIRECTOR_OPERATING_MANUAL.md
3. /docs/agent/04_QUALITY_BAR.md
4. /docs/agent/05_SECURITY_GUARDRAILS.md
5. /docs/agent/06_ARCHITECTURE_DECISIONS.md
6. /docs/agent/07_ROADMAP_INDEX.md
7. /docs/agent/status/*

Do not implement code. Coordinate roadmap sequencing, review Supervisor summaries, maintain project status, and provide exact copy-paste prompts when a new Supervisor session should start.

Start by telling me which Supervisor session to launch first and give me the exact prompt to use.
```

### Step 5: Start the Supervisor session

The Director must give you the exact Supervisor launch prompt.

That prompt should include:

- section name
- phase name, if relevant
- files to read
- what not to do
- what to do first
- how to handle user inputs
- how to report back to the Director

Example:

```text
You are the Supervisor for Section 1: Foundation, Environments, Auth & Security.

Read:
1. /docs/agent/02_SUPERVISOR_OPERATING_MANUAL.md
2. /docs/agent/04_QUALITY_BAR.md
3. /docs/agent/05_SECURITY_GUARDRAILS.md
4. /docs/agent/12_RISK_CLASS_AND_ROUTING.md
5. /docs/agent/13_VERIFICATION_GATE_PROTOCOL.md
6. /docs/agent/sections/01_foundation/SECTION_BRIEF.md
7. /docs/agent/sections/01_foundation/PHASES.md
8. /docs/agent/status/*

Do not implement code yourself. Coordinate Section 1 only. Start by checking the first phase preflight requirements. If anything is needed from the user, explain exactly what is needed, why, how to get it, where to provide it, any safety warning, and what happens next.

When a phase completes or blocks, produce a Director-ready summary.
```

### Step 6: Supervisor launches Subagents

The Supervisor launches workers with short prompts that point to task files.

Example:

```text
Read /docs/agent/sections/01_foundation/phase-01-staging-production/01_environment-inventory.md and execute every instruction. Follow verification steps. Fill the Reporting section. Commit with the specified message.
```

The task file is the source of truth. Do not duplicate full task instructions into worker prompts.

### Step 7: Paste Supervisor milestone summaries back to Director

Paste only milestone-level Supervisor output to the Director:

- phase started
- phase blocked
- phase completed
- phase gate failed
- section completed
- major decision needed
- R2/high-risk escalation

The Director then decides what happens next and gives the next exact Supervisor prompt when needed.

## Core documents

```text
01_OPERATING_MODEL.md
02_DOCUMENT_SYSTEM.md
03_DOCUMENT_CREATION_PROTOCOL.md
04_COMMUNICATION_PROTOCOL.md
05_QUALITY_BAR.md
06_SECURITY_GUARDRAILS.md
07_TASK_GRANULARITY_RULES.md
08_PHASE_PREFLIGHT_PROTOCOL.md
09_PARALLELIZATION_PROTOCOL.md
10_REPORTING_AND_STATUS_PROTOCOL.md
11_ADAPTATION_AND_EXTENSION_GUIDE.md
12_RISK_CLASS_AND_ROUTING.md
13_VERIFICATION_GATE_PROTOCOL.md
14_WORKER_STANDARDS_CARD.md
15_TASK_FILE_READINESS_RUBRIC.md
16_OPTIONAL_ENFORCEMENT_ADAPTERS.md
```

## Templates

Use the templates in `/templates` to generate a project-specific pack:

```text
PROJECT_OVERVIEW_TEMPLATE.md
DIRECTOR_OPERATING_MANUAL_TEMPLATE.md
SUPERVISOR_OPERATING_MANUAL_TEMPLATE.md
SUBAGENT_EXECUTION_RULES_TEMPLATE.md
ROADMAP_INDEX_TEMPLATE.md
SECTION_BRIEF_TEMPLATE.md
PHASE_BRIEF_TEMPLATE.md
TASK_EXECUTION_TEMPLATE.md
VERIFICATION_GATE_TASK_TEMPLATE.md
FIX_TASK_TEMPLATE.md
SUPERVISOR_REPORT_TEMPLATE.md
STATUS_FILE_TEMPLATE.md
USER_REQUEST_TEMPLATE.md
```

## Risk classes

AEOS v1.1 adds a truth layer.

Every task declares a risk class:

```text
R0 = low-risk mechanical work
R1 = normal feature/product work
R2 = high-risk work involving auth, RLS, payments, production config, secrets, migrations, webhooks, privacy, or AI-cost paths
```

R2 tasks require stronger verification, stricter reporting, and review unless explicitly waived.

## Path scope control

Every task must declare `allowed_paths`.

Workers must stay inside those paths. If another file must change, the worker stops and reports the required scope expansion instead of silently editing it.

Example:

```yaml
allowed_paths:
  - "src/app/inbox/**"
  - "src/components/job-card/**"
  - "tests/inbox/**"
```

## Evidence-backed verification

Workers must not simply say “tests passed.” They must report the command, exit code, and relevant output.

Example:

```text
Command: pnpm test
Exit code: 0
Output: 42 tests passed
```

Phase gates re-check combined work after multiple tasks complete.

## User request protocol

Every request to the user must include:

1. what is needed
2. why it is needed
3. how to get it
4. where to provide it
5. safety warning, if relevant
6. what happens next

Bad:

```text
Need Supabase keys.
```

Good:

```text
I need the Supabase staging Project URL and anon key so the staging environment can connect to the correct database.

How to get them:
1. Open Supabase.
2. Select the staging project.
3. Go to Project Settings -> API.
4. Copy Project URL and anon public key.
5. Add them to Vercel Staging as NEXT_PUBLIC_SUPABASE_URL and NEXT_PUBLIC_SUPABASE_ANON_KEY.

Do not commit these values to the repo.

Next: after these are added, the staging deployment verification task can confirm the app connects to staging Supabase.
```

## What to customize per project

AEOS is intentionally project-agnostic. Each project must extend it.

Customize:

- project overview
- architecture decisions
- quality bar extensions
- security guardrail extensions
- verification commands
- testing expectations
- UX expectations
- accessibility expectations
- deployment environments
- status files
- section/phase/task breakdown

Do not remove the core rules around scope, verification, user requests, security, and reporting.

## Golden rules

```text
The operating system is stable.
The project pack is custom.
The quality bar is inherited, then extended.
The task file is the source of truth for execution.
Gates block artifacts, not operators.
The Director provides exact Supervisor launch prompts.
The Supervisor handles task-level noise.
The Director handles roadmap-level decisions.
```
