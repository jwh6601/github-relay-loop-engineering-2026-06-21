# Safety And Hygiene

The workflow is designed for public or semi-public GitHub issue boards. Treat every board comment as potentially visible.

## Aggregate-Only Public Comments

Public comments should contain:

- status,
- counts,
- PR numbers,
- validation result,
- high-level blocker class,
- next recommendation.

Public comments should not contain:

- API keys,
- authorization headers,
- secrets,
- local absolute paths,
- temporary file paths,
- raw provider payloads,
- full generated prose,
- full prompts,
- private user data,
- unreleased project material.

## Non-Evidence

If a comment accidentally contains a path, secret-like value, raw payload, or unrelated local note, mark it as non-evidence. Later summaries should not cite it as proof of work.

## Risk Tiers

### Green

Docs, templates, eval-only tools, fixture-only changes, UI copy, narrow review.

### Amber

Test harnesses, optional UI surfaces, non-default feature flags, diagnostic tools, model-format probes.

### Red

Provider/live eval, production/default-path changes, schema changes, storage adapters, destructive operations, issue/route close, public release, production readiness claims.

Red work needs explicit Controller approval.

## Hygiene Rule

When speed and safety conflict, keep the board clean and ask for a narrow decision. A polluted board slowly destroys the entire workflow.
