---
name: github-relay-loop-engineering
description: Use when setting up, auditing, or running a multi-Codex or multi-agent engineering workflow coordinated through GitHub issue boards, especially with Controller, Loop Engineer, Dispatcher, Worker, Reviewer, and Supervisor roles. Trigger this for board-driven task queues, remote locks, phase gates, aggregate-only comments, dispatcher routing, worker prompt packs, workflow optimization, or converting a project coordination pattern into a reusable operating protocol.
---

# GitHub Relay Loop Engineering

## Overview

Use this skill to run a project through GitHub issue boards as the durable truth source while several Codex threads or agents do specialized work. The workflow optimizes for controlled parallelism: fast dispatch, short ledgers, clear phase gates, sanitized evidence, and one Controller-facing decision stream.

This skill is project-agnostic. Keep project names, repo names, issue numbers, thread ids, worker pools, and forbidden surfaces in a separate project config or board comment.

## Use This When

- The user wants a Controller/Loop Engineer/Dispatcher/Worker/Supervisor workflow.
- Several Codex threads need to share state without polluting the main Controller thread.
- A GitHub issue is being used as a task board, queue, ledger, or phase gate.
- Work is stalling because dispatch depends only on slow polling.
- The user asks to optimize, formalize, or package a loop-engineering process as a reusable skill.

Do not use this for a simple single-thread code task unless the user explicitly wants the workflow scaffold.

## Required Inputs

Before launching or changing a workflow, identify these items from the project config or the current request:

- Repository and board issue ids.
- Role registry: Controller, Loop Engineer, Dispatcher, Worker pools, Reviewer, Supervisor.
- Routing channels: thread ids if available, not titles or fuzzy names.
- Current phase objective and phase-stop condition.
- Allowed and forbidden actions: provider calls, merges, issue close, production/default path, destructive edits, external sends.
- Evidence policy: what can be posted publicly, what must remain local, and what is non-evidence.

If thread routing or GitHub state cannot be verified, stop and report the blocker. Do not guess.

## Role Model

- Controller: owns product decisions, phase gates, authorization, and final user-facing summaries.
- Loop Engineer: decomposes phase goals into quests, releases eligible work, interprets results, writes phase summaries, and stops at decision gates.
- Dispatcher: routes released work to the right worker thread, keeps a short dispatch ledger, and avoids duplicate sends.
- Worker: claims exactly one eligible quest, creates a lock first, completes the task, posts an aggregate-only result, then stops.
- Reviewer: performs focused review or green-lane review when explicitly released.
- Supervisor: audits workflow health, over-dispatch, under-dispatch, boundary drift, hygiene leaks, and missing controller notifications.

Do not collapse these roles unless the user asks for a lighter workflow.

## Optimized Loop

Apply all ten optimizations by default:

1. Separate short ledger from long evidence. Board comments should carry compact state; detailed evidence belongs in PRs, files, or linked artifacts.
2. Maintain a fixed board state summary: active quests, locked quests, open PRs, merged PRs, blockers, held gates, next decision.
3. Prefer event-first routing. Loop Engineer or worker should notify Dispatcher after posting a release/result; heartbeat is fallback only.
4. Use risk tiers. Low-risk docs/eval/UI polish can proceed with narrow review; provider, production, default-path, schema, storage, and destructive actions need explicit authorization.
5. Keep a role registry. Route by stable ids, not display names or thread titles.
6. Use short worker prompts. The worker gets a pointer to the board, one quest id, lock rules, result format, and safety boundary.
7. Define phase gates before fan-out. A phase must state what counts as done, what blocks it, and when Controller must decide.
8. Use Controller-ready summaries. Report whether the thing works, the current quality level, main risks, cost/speed impact, and the next decision.
9. Clean up superseded work. Mark superseded PRs/tasks clearly; do not leave duplicate branches or ambiguous candidates alive.
10. Separate reusable workflow from project config. The skill defines process; the project board defines current facts.

## Templates

Use the repository `templates/` directory for board comments, worker point-calls, phase summaries, controller decisions, and supervisor audits.
