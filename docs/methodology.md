# Methodology

GitHub Relay Loop Engineering is a coordination pattern for AI-native engineering teams. It assumes that many agents can produce useful work, but that unmanaged autonomy creates duplicate work, hidden drift, and unreadable logs.

The method has three design principles:

1. **GitHub is the shared truth source.** Chats are execution surfaces; the board is the durable ledger.
2. **Autonomy is tiered.** Low-risk work can move quickly. High-risk work stops at a phase gate.
3. **The human receives decisions, not raw exhaust.** The Controller summarizes whether the thing works, what changed, what remains risky, and what decision is needed.

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

## Ten Default Optimizations

1. Separate short ledger comments from long evidence.
2. Keep a fixed board state summary.
3. Prefer event-first routing, with heartbeat as fallback.
4. Classify work by risk tier.
5. Route by stable role and thread ids, not fuzzy titles.
6. Use short worker prompts with one quest only.
7. Define phase gates before fan-out.
8. Write Controller-ready summaries.
9. Mark superseded PRs, branches, and quests clearly.
10. Keep reusable workflow separate from project-specific config.

## When To Stop

Stop worker fan-out when:

- the next step is a product decision,
- evidence is inconclusive and more mechanical testing is not useful,
- production/default-path work would be next,
- provider/live eval would be next,
- a route or issue close would be next,
- a supervisor finds boundary drift or hygiene risk.

Stopping is not failure. It is how the workflow preserves product ownership.
