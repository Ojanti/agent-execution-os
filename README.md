# Agent Execution OS

Agent Execution OS is a reusable operating system for coordinating AI agents through complex software/product work.

It is designed for projects where one strong coordinating agent directs cheaper execution agents without losing quality, scope control, or safety.

## Core operating model

```text
Director reads the world.
Supervisor reads the section and tracks phases + task progression.
Subagent reads the task + standards and executes.
```

## What v1.1 adds

v1 documented process. v1.1 adds a truth layer.

That means:

- every task declares risk class: `R0`, `R1`, or `R2`
- every task declares `allowed_paths`
- workers cannot drift outside scope silently
- verification requires raw output and exit codes
- phase gates re-check combined work
- R2 work gets stricter review and clean-checkout verification
- optional adapters can enforce the protocol, but the core remains markdown-first and tool-agnostic

## When to use AEOS

Use AEOS when:

- work spans many files/phases
- AI agents may run in parallel
- you need strong coordination
- you want cheaper subagents to execute safely
- quality/security drift is costly
- user inputs, accounts, keys, or approvals may block phases
- you want reusable planning and execution docs across projects

Do not use AEOS for tiny one-off edits where the process overhead is larger than the work.

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
AEOS_v1.1_SPEC.md
CHANGELOG.md
MANIFEST.md
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

## Optional adapter

The included Cursor adapter is here:

```text
optional/cursor-enforcement/
```

It is a reference implementation, not doctrine.

Core AEOS is portable. Adapters are swappable.

## Basic adoption flow

1. Read the core docs.
2. Adapt the templates into your project under `/docs/agent/`.
3. Extend the quality/security bars for your project type.
4. Create a roadmap index with sections and phases.
5. Write fully detailed task files only for the first execution phase.
6. Ensure every task passes the readiness rubric.
7. Run Director → Supervisor → Subagent execution.
8. Use phase verification gates before accepting phase completion.

## Golden rules

```text
The operating system is stable.
The project pack is custom.
The quality bar is inherited, then extended.
The task file is the source of truth for execution.
Gates block artifacts, not operators.
```
