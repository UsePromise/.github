---
name: privacy-impact-review
description: Review new Promise features and data flows for privacy, retention, provenance, consent, and least-privilege risks before launch.
---

# Privacy Impact Review

Map the proposed data flow end to end.

Identify:
- data collected, inferred, generated, retained, and deleted
- source and user expectation
- account/tenant boundary
- processors and external providers
- OAuth/API scopes required
- whether sensitive content is copied into logs, analytics, prompts, caches, or support tooling
- retention and deletion behavior
- whether derived memories/signals retain source provenance
- user controls and consequences of disconnect/delete

Challenge collection that is merely convenient. Prefer least privilege and data minimization. Do not weaken explicit-send or consequential-action approval without a separately reviewed policy.

## Output

State data-flow changes, new trust assumptions, least-privilege concerns, retention/deletion implications, required user disclosure/control, and unresolved launch blockers. Distinguish legal questions requiring counsel from product/engineering privacy risks that can be fixed directly.
