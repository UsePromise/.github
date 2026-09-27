# Promise operating system

Promise is intentionally designed to remain operable by one human for as long as practical.

This document explains how the company-wide agent, skill, instruction, governance, and human-judgment layers fit together. It is the all-up map of the Promise operating model. Repository-local `AGENTS.md` files remain authoritative for local implementation details.

## Goal

The purpose of the Promise operating system is not simply to make one person produce more work. It is to keep the company small by continually reducing the amount of work, coordination, infrastructure, conceptual surface area, and recurring manual operation that the company requires.

Agents should therefore optimize for leverage and simplification, not throughput alone.

Core principles:

- Minimize permanent operational, architectural, and conceptual complexity.
- Prefer deletion, consolidation, and reuse over addition.
- Treat every new service, queue, datastore, cache, scheduled job, dependency, framework, repository, setting, feature flag, vendor, workflow, and user-facing concept as ongoing operating cost.
- Keep one canonical owner for state and business rules.
- Preserve privacy, authorization, account isolation, provenance, and explicit user control.
- Keep public claims bounded by shipped and enabled capability.
- Consider failure, cost, and operational behavior at materially larger scale.
- For every meaningful addition, ask what can be removed, collapsed, or made unnecessary.
- Turn recurring founder/operator work into deterministic or automated workflows where practical.
- Scale by removing coordination, not by recreating organizational structure in software.

## Operating hierarchy

The layers are intentionally different. Do not use agents or prose where a deterministic control is possible, and do not put every judgment into CI.

```text
Company principles
    ↓
Repository AGENTS.md + Copilot instructions
    ↓
Path-specific automatic instructions
    ↓
Skills
    ↓
Specialist agents
    ↓
Deterministic governance / CI where possible
    ↓
Human judgment
```

### Company principles

The stable philosophy of how Promise should be built and operated. These are defined here and reflected in repository-local instructions.

### Repository instructions

Each product repository keeps concise always-on instructions in `AGENTS.md` and `.github/copilot-instructions.md`.

They define:

- what the repository owns and must not own
- local architectural and product invariants
- company-wide invariants expressed in local terms
- authoritative docs
- validation expectations
- relevant skills and specialist roles

Critical rules are intentionally duplicated locally. A rule that must apply on every task must not depend on cross-repository discovery.

### Path-specific instructions

`.github/instructions/*.instructions.md` files automatically add stronger policy when particular files are in scope.

Examples include database/state, mail/provider integrations, infrastructure, iOS services/models/views, public marketing claims, and trust/legal surfaces.

### Skills

Skills are reusable procedures: how to perform a class of work well.

Use a skill when a task needs a repeatable method, evidence standard, review procedure, or structured checklist. Prefer adding or improving a skill before creating another agent.

Company-wide skills live in `UsePromise/.github/skills/`. Implementation-specific skills stay in the repository that owns the implementation.

### Specialist agents

Agents are durable company roles with distinct judgment, context, and escalation behavior. They are not the primary mechanism by which policy becomes active.

Agents should load and obey repository-local instructions and apply relevant skills.

### Deterministic governance and CI

Anything mechanically detectable should move into code or CI over time.

Examples:

- forbidden architecture crossings
- dependency growth requiring rationale
- new structural/runtime surfaces requiring rationale
- generated contract drift
- migration/schema changes requiring rollback thinking
- public capability changes requiring evidence
- direct provider/datastore coupling where a client boundary forbids it

Natural-language policy guides judgment. CI enforces structural facts.

### Human judgment

The human founder remains the final decision-maker for product direction, material tradeoffs, irreversible commitments, and exceptions where the automated system cannot safely determine the right answer.

The operating system should surface those decisions clearly rather than quietly making them on the founder's behalf.

## What lives where

### `UsePromise/.github`

The declarative company operating system:

- company-wide agents
- company-wide skills
- operating principles
- recurring company rituals
- shared governance philosophy
- this document

It should not accumulate repository-specific implementation detail.

### `UsePromise/platform`

Canonical backend and domain owner:

- API and worker behavior
- canonical business rules
- database/schema/migrations
- provider integration
- authorization and provenance
- queues/background processing
- production infrastructure
- platform contracts

Client repositories consume the platform; they do not recreate it.

### `UsePromise/ios`

Native Promise client:

- Swift app and native UX
- account-safe client state/cache behavior
- native DTOs/contracts
- widgets/extensions
- native tests
- TestFlight/App Store release pipeline

It must not become a second backend or second source of canonical business truth.

### `UsePromise/site`

Public acquisition and trust surface:

- marketing/product explanation
- SEO/discovery
- pricing copy
- public capability claims
- privacy/security/legal/support pages
- marketing-site deployment

It explains Promise; it does not reimplement Promise.

### `UsePromise/promise-mcp`

Thin agent-facing client over the platform API:

- MCP discovery and connection flow
- agent-friendly tool surface
- scoped client authorization flow
- composition of platform capabilities

It must not own canonical state, provider access, or backend business rules.

## Agent roster

| Agent | Primary judgment |
| --- | --- |
| Chief of Staff | priorities, open loops, company review, risks, decision hygiene, recurring operating work |
| Product Critic | product scope, UX coherence, feature pressure, positioning, concept discipline |
| Engineering Steward | architecture, scale, complexity, state ownership, operability, long-term technical shape |
| PR Reviewer | consequential implementation review across repositories |
| Mail Platform Reviewer | mail-provider integration, sync, identity, auth, mutation safety, reliability, privacy |
| Growth | acquisition, messaging, experiments, funnel reasoning, evidence-backed growth work |
| Customer Operations | support, recurring confusion, customer signals, retention/churn patterns, feedback loops |
| Trust Steward | privacy, security, data handling, permissions, public claims, trust-sensitive changes |
| Finance & Operations | vendor spend, cloud economics, recurring costs, operational leverage, company sustainability |

Add an agent only when a genuinely durable role with distinct judgment and escalation behavior has emerged.

## Skill model

A skill is preferable when the need is a procedure rather than a role.

Current company-wide skills include:

- `architecture-change-gate`
- `complexity-budget`
- `delete-before-add`
- `cost-of-scale-review`
- `product-scope-gate`
- `weekly-company-review`
- `roadmap-pruning`
- `customer-signal-synthesis`
- `privacy-impact-review`
- `public-claim-verification`
- `vendor-cost-review`

Repo-local examples include:

- `repo-forensics`
- `promise-product`
- `promise-change-review`
- `mail-platform-safety`
- `ios-client-safety`
- `promise-marketing-copy`

## Governance model

Not all controls have the same force.

| Layer | Behavior |
| --- | --- |
| Company/repo instructions | always-on guidance in supported agent surfaces |
| Path-specific instructions | automatically routed based on files in scope |
| Skills | deeper procedure loaded/applied when relevant |
| Agents | specialist judgment and routing |
| Governance CI | deterministic pass/fail for mechanically detectable rules |
| Branch protection | converts CI into a hard merge gate when required checks are configured |

A rule is not truly hard-enforced until a deterministic check exists and the repository requires that check before merge.

## Complexity policy

For any material change, explicitly consider:

1. What permanent complexity does this add?
2. What does it replace, delete, collapse, or make unnecessary?
3. Who or what owns the resulting state?
4. What new recurring operation does this create?
5. Can that operation be automated or eliminated?
6. How does the design behave at materially larger scale?
7. What happens when dependencies, providers, retries, or partial failures behave badly?
8. Is the product gaining a new concept that users or the founder must now understand forever?

The default is not "never add complexity." The default is "make its lifetime cost explicit before accepting it."

## Evolution rule

Use this progression when the operating system encounters repeated work or repeated failure:

```text
Repeated mistake or overlooked rule
    → instruction

Repeated procedure
    → skill

Recurring distinct judgment role
    → agent

Mechanically detectable invariant
    → deterministic CI/test

Repeated founder operation
    → automation/loop
```

Do not create a new agent because a task feels specialized once. Do not create another repository because a category exists conceptually. Let repeated evidence justify new structure.

## Adding a new repository

Every new Promise product repository should start with:

1. A concise `AGENTS.md` defining ownership, boundaries, invariants, and validation.
2. `.github/copilot-instructions.md` containing the critical always-on rules.
3. Path-specific instruction files for high-risk areas where useful.
4. Repo-local skills only for implementation-specific procedures.
5. A governance workflow for mechanically detectable architecture/trust/complexity rules.
6. A PR template exposing any rationale/evidence fields required by governance.
7. A pointer back to this document.
8. Clear identification of the canonical upstream owner for domain state and contracts.

Before creating the repository, apply the architecture and complexity gates and explain why the work cannot remain inside an existing boundary.

## Known limitations

- Natural-language instructions are probabilistic; they can guide but do not guarantee behavior.
- Cross-repository discovery may vary by tool/runtime, which is why critical invariants are repeated locally.
- Deterministic checks can only enforce what can be detected reliably without excessive false positives.
- Governance CI is only a hard merge gate when branch protection/rules require it.
- The central `.github` repository should remain primarily declarative. If substantial executable cross-company orchestration emerges, a separate executable `company-os` repository may eventually become justified.

## Source of truth

This document is the all-up map. `AGENT-STRATEGY.md` describes the agent/skill design in more detail. Individual repositories remain authoritative for their local architecture, implementation, runtime, and validation rules.
