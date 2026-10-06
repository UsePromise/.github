# Promise company skills

This repository is the declarative operating system for Promise as a one-human company.

## Placement rule

Canonical company skills live in this repository at `.github/skills/<skill-name>/SKILL.md`. Copilot discovers exactly that one-level path in the repository being worked in. It does not inherit skills from the organization `.github` repository into product repositories, and it does not discover `skills/<family>/<skill-name>/`.

Put a procedure here when it remains useful even if a product repository disappears. Put a skill inside a product repository when it depends on specific files, commands, architecture, runtime behavior, or release mechanics.

To load a company skill while working in a product repository, copy its directory to that repository's `.github/skills/<skill-name>/`. Organization agents must read `UsePromise/.github` at `.github/skills/<skill-name>/SKILL.md` when the local copy is absent. Do not assume the skill is already in context.

## Design rule

Prefer skills over new agents. Add a new agent only when a durable role needs distinct judgment, priorities, and escalation behavior. Add a skill when the work is a repeatable procedure.

## Company-wide principles

- Every new capability must justify its permanent operational cost.
- Every abstraction must remove more complexity than it introduces.
- Every recurring process should first be considered for automation.
- Every vendor or external dependency should have an exit path.
- Every feature should identify what it replaces, collapses, or makes unnecessary.
- Scale by removing coordination rather than creating organizational structure.
- Preserve explicit human approval for consequential external actions unless a deliberate policy says otherwise.

## Current skills

Families are labels, not directories. Every skill directory is directly under `.github/skills/`.

- Company: `weekly-company-review`, `roadmap-pruning`
- Product: `product-scope-gate`
- Engineering: `architecture-change-gate`, `complexity-budget`, `delete-before-add`, `cost-of-scale-review`, `review-findings`
- Customer: `customer-signal-synthesis`
- Trust: `privacy-impact-review`, `public-claim-verification`
- Finance: `vendor-cost-review`
