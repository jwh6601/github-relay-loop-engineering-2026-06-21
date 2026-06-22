# GitHub Relay Loop Engineering Templates

Use the repository-level `templates/` directory as the source of truth for reusable board comments and role prompts. When this folder is installed as a Codex skill, load the smallest template needed for the current task:

- `templates/project-config.example.yaml`
- `templates/board-state.md`
- `templates/local-board-snapshot.md`
- `templates/quest-release.md`
- `templates/worker-point-call.md`
- `templates/quest-result.md`
- `templates/dispatcher-action.md`
- `templates/phase-summary.md`
- `templates/controller-decision.md`
- `templates/supervisor-audit.md`
- `templates/superseded-work.md`

Keep project-specific issue numbers, thread ids, repository names, and forbidden surfaces outside the reusable skill body.
