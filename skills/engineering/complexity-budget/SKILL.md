---
name: complexity-budget
description: Quantify and challenge the permanent complexity introduced by a feature, technical change, or operating decision.
---

# Complexity Budget

Treat complexity as a scarce company resource because Promise is intended to remain a one-human company as long as possible.

## Inventory the change

Count newly introduced or materially expanded:
- user-facing concepts and settings
- deployables and runtimes
- databases, tables, queues, caches, scheduled jobs, flags, secrets, and providers
- packages, repos, frameworks, and external dependencies
- operational alerts, dashboards, runbooks, and manual procedures
- recurring business processes
- cross-repo coordination steps

Do not optimize the score mechanically. Use the inventory to reveal permanent obligations.

## Challenge

For each addition ask:
- Can an existing concept absorb this?
- Is this permanent or rollout-only?
- Can it be generated, derived, or deleted after migration?
- Does it require human memory or recurring manual attention?
- What is the failure/maintenance burden at 10x scale?

## Output

Summarize complexity added, complexity removed, net permanent obligations, and the smallest simplification that preserves the outcome. Flag any change that creates recurring founder work without an automation path.
