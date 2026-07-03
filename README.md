# IT Agent

`IT Agent` is a local-first open-source agent design for building tools and systems with a small set of focused subagents.

This repository is the public OSS surface of `it-agent` itself.
The surrounding daily factory that improves it lives separately and is not the product being distributed.

## What It Is

`IT Agent` is designed around one orchestrating agent plus a small permanent subagent set:

- `builder`
- `tester`
- `reviewer`
- `uiux`
- `improver`

The goal is not to create many agent names.
The goal is to keep a compact team structure and continuously improve the quality of each role.

## Core Principles

- Local-first: outputs should be runnable locally first
- Small role set: only keep roles that are repeatedly useful
- Visible improvement loop: feedback should update the agent standard
- UI/UX matters: tools should be understandable, usable, and demo-ready
- Principles over templates: improve judgment and review criteria, not fixed visual patterns

## Current State

This repository currently contains:

- role definitions
- subagent architecture docs
- handoff contracts
- review and UI/UX checklists
- `.codex` subagent configuration
- reflection logs
- a sample run that shows handoff shape

This repository does not yet contain a fully packaged end-user runtime.
Right now, it is the public source of truth for how `IT Agent` is structured and how it evolves.

## Repository Structure

```text
.codex/
  agents/                Subagent definitions
checklists/             Reusable review checklists
docs/                   Architecture, rules, roadmap, handoff docs
logs/                   Reflection history
runs/sample-run/        Example handoff artifacts
```

## How The Agent Is Organized

### Permanent Roles

- `builder`: implements local-first tools and systems
- `tester`: verifies launch, happy path, and failure path behavior
- `reviewer`: checks quality, regressions, and OSS clarity
- `uiux`: improves clarity, usability, and demo strength
- `improver`: turns findings into `reflect / hold / reject`

### Conditional Specialists

Language or domain specialists are allowed only when repeatedly justified.

Examples:

- `python-specialist`
- `ts-specialist`

The rule is: improve the existing system first, add new roles only when the same class of problem keeps repeating.

## Key Documents

- [Agent Composition Rules](./docs/agent-composition-rules.md)
- [Subagents Architecture](./docs/subagents-architecture.md)
- [Handoff Contract](./docs/handoff-contract.md)
- [UIUX Review Checklist](./docs/uiux-review-checklist.md)
- [Reflection Policy](./docs/reflection-policy.md)
- [Roadmap](./docs/roadmap.md)

## Sample Flow

```text
it-agent
-> builder
-> tester
-> reviewer
-> uiux
-> improver
-> reflection into the IT Agent standard
```

You can inspect a sample handoff sequence in [runs/sample-run](./runs/sample-run/README.md).

## Philosophy For UI And Demo Evolution

`IT Agent` should improve not only code quality, but also how tools are presented.

- UI and video quality are part of product quality
- Reusable principles are welcome
- Fixed visual templates are not the goal
- Each run should still choose the best format for that specific tool

## Intended OSS Use

This repository is suitable for people who want to:

- study a compact subagent architecture
- reuse the role split and handoff model
- adapt the checklists for their own local-first tool builder
- evolve an agent system through documented reflection

## License

This repository is released under the MIT License.

