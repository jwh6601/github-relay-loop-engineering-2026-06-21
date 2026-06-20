# Dispatcher Action

```text
dispatcher_action:
- trigger: [release/result/gate/comment id]
- target_role: [worker type]
- target_thread_id: [stable id]
- quest_id: [id]
- reason: [one sentence]
- dedupe_basis: [latest prior action checked]
- safety: aggregate-only
```
