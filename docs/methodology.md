# Methodology

GitHub Relay Loop Engineering is a coordination pattern for AI-native engineering teams. It assumes that many agents can produce useful work, but that unmanaged autonomy creates duplicate work, hidden drift, and unreadable logs.

The method has three design principles:

1. **GitHub is the shared truth source.** Chats are execution surfaces; the board is the durable ledger.
2. **Autonomy is tiered.** Low-risk work can move quickly. High-risk work stops at a phase gate.
3. **The human receives decisions, not raw exhaust.** The Controller summarizes whether the thing works, what changed, what remains risky, and what decision is needed.

For mature boards, the method also uses a token-efficient hybrid relay: local status docs or board snapshots are fast caches, while GitHub issues, PRs, remote locks, and GitHub CI remain authoritative.

## Roles

### Controller

The Controller is the human-facing executive layer. It owns product judgment, authorization, and final summaries. It should not drown in worker logs.

### Loop Engineer

The Loop Engineer turns a phase objective into quests, reads results, releases follow-up work, and stops at phase gates.

### Dispatcher

The Dispatcher routes released tasks to the right workers. It should be lightweight, event-driven when possible, and quiet when nothing changed.

### Worker

A Worker performs exactly one eligible quest. It refreshes the board, creates a lock, claims the quest, completes it, posts an aggregate result, then stops.

### Reviewer

A Reviewer performs focused review, green-lane review, or merge-readiness checks when explicitly released.

### Supervisor

The Supervisor audits process health: stalled boards, over-dispatch, missing controller notifications, hygiene issues, and boundary drift.

## Default Optimizations

1. Separate short ledger comments from long evidence.
2. Keep a fixed board state summary.
3. Add a local board snapshot for large boards so workers do not reread the full issue history.
4. Prefer event-first routing, with heartbeat as fallback.
5. Classify work by risk tier.
6. Route by stable role and thread ids, not fuzzy titles.
7. Use short worker prompts with one quest only.
8. Define phase gates before fan-out.
9. Write Controller-ready summaries.
10. Mark superseded PRs, branches, and quests clearly.
11. Keep reusable workflow separate from project-specific config.

## Hybrid Relay Read Order

For large boards, use this default read order:

1. Stable protocol and current status.
2. Local board snapshot, if present and fresh.
3. Assigned release/result/comment ids.
4. Exact remote lock ref.
5. Target PR files, review state, and CI.
6. Full GitHub issue history only when the snapshot is stale, missing, contradictory, or the task is an audit.

The goal is to spend tokens on the task, not on repeatedly rereading the same board. In real comment-heavy boards, this can cut coordination context by roughly 80-90% while preserving auditability.

## CI Evidence

Local tests and builds are preflight evidence. GitHub PR CI is merge-readiness evidence. Post-merge GitHub main CI is phase-gate evidence.

## When To Stop

Stop worker fan-out when:

- the next step is a product decision,
- evidence is inconclusive and more mechanical testing is not useful,
- production/default-path work would be next,
- provider/live eval would be next,
- a route or issue close would be next,
- a supervisor finds boundary drift or hygiene risk.

Stopping is not failure. It is how the workflow preserves product ownership.
