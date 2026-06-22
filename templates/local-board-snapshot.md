# Local Board Snapshot

Use this as a local speed cache for a large GitHub board. It does not replace GitHub.

```text
local_board_snapshot:
- board: [phase id]
- issue: #[number]
- last_refreshed: [timestamp]
- snapshot_status: [fresh / stale / needs_github_refresh]
- authoritative_source: GitHub issue / PR / remote locks / GitHub CI
- phase: [name]
- objective: [one sentence]
- current_verdict: [working / blocked / inconclusive / parked]
- latest_controller_decision: [comment id and one sentence]
- active_or_authorized_quests: [quest ids]
- locked_or_claimed: [quest ids and lock owners]
- open_prs: [number, draft/ready, CI, mergeability, next action]
- merged_prs: [number and scope]
- blockers: [short list]
- held_gates: [provider / production / schema / close / other]
- worker_read_targets:
  - [exact comment ids]
  - [target PRs]
  - [exact lock refs]
  - [CI run ids if relevant]
- next_controller_decision: [one sentence]
- rule: if this snapshot and GitHub disagree, GitHub wins
```

Workers may use this snapshot for orientation, but must still verify the assigned release/result comments, exact lock ref, target PR state, and GitHub CI before claiming, reviewing, merging, or reporting a phase gate.
