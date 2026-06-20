# GitHub Relay Loop Engineering

A lightweight, board-driven workflow for coordinating multiple AI coding agents through GitHub issues.

This repository packages a practical method, templates, and a Codex skill for running multi-agent engineering work without turning the main planning conversation into a giant log stream.

## What It Solves

Multi-agent coding often fails for boring reasons:

- agents duplicate work,
- nobody knows which task is truly claimed,
- evidence is scattered across chats,
- managers read too many raw logs,
- workers keep going past the decision point,
- high-risk actions happen before the human owner has actually approved them.

GitHub Relay Loop Engineering uses GitHub issues as the durable coordination layer. Chats can come and go, but the board remains the truth source.

## Core Idea

Use separate roles:

- **Controller** decides product direction and phase gates.
- **Loop Engineer** decomposes the phase into concrete quests.
- **Dispatcher** routes released quests to workers and prevents duplicate sends.
- **Workers** claim one task, do it, report an aggregate result, then stop.
- **Reviewers** handle focused review or green-lane review.
- **Supervisor** audits whether the workflow is stuck, overactive, or drifting.

The result is a workflow where the human can talk to one Controller thread while many agents work in parallel behind a GitHub board.

## Repository Layout

```text
docs/
  methodology.md
  workflow.md
  safety-and-hygiene.md
templates/
  project-config.example.yaml
  board-state.md
  quest-release.md
  worker-point-call.md
  quest-result.md
  dispatcher-action.md
  phase-summary.md
  controller-decision.md
  supervisor-audit.md
codex-skill/
  github-relay-loop-engineering/
```

## Quick Start

1. Create a GitHub issue for the phase board.
2. Fill `templates/project-config.example.yaml` with repo, board, role, and boundary data.
3. Ask the Loop Engineer to post quest releases on the board.
4. Let Dispatcher route only released, dependency-satisfied, unlocked quests.
5. Workers post aggregate-only quest results.
6. Loop Engineer writes a phase summary when the phase reaches a decision point.
7. Controller decides whether to continue, narrow, pause, merge, park, or close.

## Non-Goals

This is not a full autonomous software company. It is also not a replacement for judgment, product ownership, or code review.

This method deliberately keeps high-risk actions behind explicit gates: production/default-path changes, provider calls, destructive operations, public release, secret handling, route closure, and production readiness claims.

## Status

Experimental, extracted from real multi-agent project operations and packaged as a reusable method plus prompt/template set.

## License

MIT. See `LICENSE`.
