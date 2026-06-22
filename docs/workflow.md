# Workflow

## 1. Open A Phase Board

Create a GitHub issue for one phase. The issue should contain:

- phase objective,
- completion criteria,
- hard holds,
- role registry,
- evidence policy,
- current board state summary.

Do not mix unrelated phases on one board unless the project is tiny.

## 2. Create Or Refresh A Local Snapshot

For a large board, create a local board snapshot before fanning out work. The snapshot should contain:

- current phase,
- latest controller decision,
- active or authorized quests,
- locks and claims,
- open and merged PRs,
- blockers,
- held gates,
- exact worker read targets.

The snapshot is a speed cache only. If the snapshot and GitHub disagree, GitHub wins.

## 3. Release Quests

The Loop Engineer posts `quest_release` comments. A release must state:

- quest id,
- worker type,
- dependencies,
- allowed scope,
- risk tier,
- required output,
- phase-stop relevance.

## 4. Route Work

Dispatcher routes only quests that are:

- released,
- dependency-satisfied,
- unlocked,
- within the worker type,
- inside the authorized risk tier.

Dispatcher should write a short `dispatcher_action` entry after sending a worker prompt.

## 5. Claim And Execute

Worker reads the local snapshot first if one exists, then verifies the assigned release/result comments, target PR state, GitHub CI, and remote locks. If the quest is still eligible, it creates a lock before posting claim.

The worker completes the task and posts `quest_result`.

## 6. Review Or Continue

Loop Engineer reads results and either:

- releases the next quest,
- requests focused review,
- marks the work blocked,
- supersedes duplicate work,
- writes a phase summary.

## 7. Gate

When a phase reaches a decision point, Loop Engineer writes `phase_summary / gate_request`.

Dispatcher stops worker fan-out until Controller decides.

At the gate, update the local snapshot and cite GitHub PR/CI evidence. Local tests/builds are preflight only; GitHub PR CI and post-merge main CI are the durable merge and phase-gate evidence.

## 8. Decide

Controller posts `controller_decision`:

- continue,
- narrow,
- pause,
- park,
- merge,
- close,
- open successor phase.

The decision becomes the next truth source for Loop Engineer and Dispatcher.
