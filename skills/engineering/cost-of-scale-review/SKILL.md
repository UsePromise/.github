---
name: cost-of-scale-review
description: Estimate how a product or architecture decision behaves economically and operationally as Promise usage grows.
---

# Cost of Scale Review

Evaluate variable and step-function costs before a feature becomes difficult to unwind.

Model at current scale, 10x, and 100x where meaningful:
- LLM/token calls and retry amplification
- provider/API calls and rate limits
- storage growth and retention
- database/query amplification
- queues and worker concurrency
- network/egress
- notifications and scheduled work
- third-party per-user/per-event pricing
- support and manual-review load

Separate marginal user value from marginal infrastructure cost. Look for work that scales with messages, history, contacts, or background polling rather than active product value.

Identify thresholds that would require a new runtime, vendor tier, partitioning strategy, or manual operation.

## Output

State the dominant cost drivers, likely nonlinear thresholds, cheap mitigations available now, and what should be measured in production. Do not recommend premature distributed architecture when instrumentation or bounded work is enough.
