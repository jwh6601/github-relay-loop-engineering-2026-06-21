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

## 2. Release Quests

The Loop Engineer posts `quest_release` comments. A release must state:

- quest id,
- worker type,
- dependencies,
- allowed scope,
- risk tier,
- required output,
- phase-stop relevance.

## 3. Route Work

Dispatcher routes only quests that are:

- released,
- dependency-satisfied,
- unlocked,
- within the worker type,
- inside the authorized risk tier.

Dispatcher should write a short `dispatcher_action` entry after sending a worker prompt.

## 4. Claim And Execute

Worker refreshes the board and remote locks. If the quest is still eligible, it creates a lock before posting claim.

The worker completes the task and posts `quest_result`.

## 5. Review Or Continue

Loop Engineer reads results and either:

- releases the next quest,
- requests focused review,
- marks the work blocked,
- supersedes duplicate work,
- writes a phase summary.

## 6. Gate

When a phase reaches a decision point, Loop Engineer writes `phase_summary / gate_request`.

Dispatcher stops worker fan-out until Controller decides.

## 7. Decide

Controller posts `controller_decision`:

- continue,
- narrow,
- pause,
- park,
- merge,
- close,
- open successor phase.

The decision becomes the next truth source for Loop Engineer and Dispatcher.
