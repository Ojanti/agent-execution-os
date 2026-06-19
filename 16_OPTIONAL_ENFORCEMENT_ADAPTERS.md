# 16. Optional Enforcement Adapters

## Purpose

Agent Execution OS core is markdown-first and tool-agnostic. Enforcement adapters are optional implementations for specific environments.

The core protocol is durable. Adapters are disposable.

## Core vs adapter

### Core

Core AEOS defines:

- roles
- document hierarchy
- task metadata
- risk classes
- `allowed_paths`
- verification evidence
- gate semantics
- communication protocol
- quality/security rules

Core is not tied to Cursor, Claude, GitHub Actions, shell scripts, or any vendor.

### Adapter

An adapter may implement AEOS using:

- Cursor rules
- hooks
- shell scripts
- CI jobs
- model binding files
- skills/instruction bundles
- GitHub Actions
- local scripts

Adapters may rot as tools change. Replace them without rewriting the core protocol.

## Included adapter

This package includes:

```text
optional/cursor-enforcement/
```

It is a reference adapter, not mandatory doctrine.

It may include:

- `.cursor/rules/*`
- `.cursor/hooks/*`
- `skills/*`
- `model-bindings.yaml`
- adapter-specific README

## Model binding

Core docs use roles:

```text
director
supervisor
worker
r2_reviewer
```

Concrete models belong in an adapter or project config.

Do not hardcode model names or cost claims in core docs.

## Gate implementation options

A project may enforce gates with:

- manual review only
- Cursor hooks
- GitHub Actions
- local scripts
- CI pipeline
- custom orchestration

The protocol remains the same:

```text
Gates block artifacts, not operators.
```

## Adapter adoption checklist

Before using an adapter:

- [ ] Confirm it matches your operating system and tools.
- [ ] Confirm scripts work on your machine/CI.
- [ ] Confirm model bindings are current and affordable.
- [ ] Confirm hooks do not block the operator from recovering.
- [ ] Confirm failures produce clear evidence.
- [ ] Confirm waivers can be logged.

## Adapter maintenance rule

If the adapter conflicts with the core, the core wins.

If the adapter becomes unreliable, disable or replace the adapter. Do not weaken the core protocol.
