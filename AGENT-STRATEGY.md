# Promise agent strategy

Promise should use a small number of durable agents backed by reusable skills, with company invariants embedded into repository instructions so they apply without explicit invocation.

The goal is not to create a persona for every task. The goal is to make high-value judgment repeatable while keeping implementation knowledge close to the repositories that own it and keeping Promise operable by one human for as long as practical.

## Enforcement hierarchy

Use four layers. Each has a different job:

1. **Always-on repository instructions** — non-negotiable product, architecture, trust, and one-human-company invariants. These belong in `AGENTS.md` and `.github/copilot-instructions.md` in each product repository.
2. **Path-specific automatic instructions** — stronger rules for high-risk areas such as database/state, mail/provider integration, infrastructure, native services/models/views, and public/trust copy. These belong in `.github/instructions/*.instructions.md` with `applyTo` globs.
3. **Skills** — deeper reusable procedures for reasoning through a class of work. Skills provide method, evidence requirements, and review structure; the critical invariant must not exist only inside the skill.
4. **Agents** — durable judgment roles and routing. Agents should invoke or apply relevant skills, but policy must not depend on a human remembering to select a particular agent.

Anything mechanically enforceable should eventually move one step further into deterministic CI/tests. Natural-language policy guides judgment; CI should enforce structural facts when practical.

## Company-wide always-on invariants

Every Promise repository should preserve these principles in its local instructions:

- Minimize permanent operational, architectural, and conceptual complexity.
- Prefer deletion, consolidation, and reuse over addition.
- Treat new services, queues, datastores, caches, scheduled jobs, frameworks, dependencies, repositories, settings, flags, concepts, vendors, and recurring processes as ongoing operating cost.
- Keep one canonical owner for state and business rules.
- Consider failure, cost, and operational behavior at materially larger scale.
- Preserve privacy, authorization, account isolation, provenance, and explicit user control.
- Keep public claims bounded by shipped and enabled capability.
- For every meaningful addition, ask what can be removed, collapsed, or made unnecessary.
- Turn recurring founder/operator work into deterministic or automated workflows where practical.

These apply whether or not a named skill or specialist agent is explicitly invoked.

## Repository instructions: local truth

Each repository owns a concise `AGENTS.md` plus `.github/copilot-instructions.md` describing:

- what the repository owns and must not own
- company-wide invariants in local terms
- authoritative architecture/product docs
- critical implementation invariants
- the smallest correct validation commands
- which organization-level skills are relevant
- which path-specific instruction files add automatic policy for particular areas

Repository-local instructions are intentionally duplicated at the invariant level. Do not rely on cross-repository discovery for rules that must be present on every task.

## Path-specific instructions

Use `.github/instructions/*.instructions.md` when a rule can be automatically routed from the files in scope. Examples:

- platform database/state → state ownership, migration safety, tenant scoping
- platform mail/provider code → parity, idempotency, unknown mutation outcomes, explicit sending
- platform infrastructure/workflows → complexity/cost/rollback/automation
- product web/native views → product-scope and concept-budget discipline
- iOS services/models → account isolation and contract safety
- site public copy → capability verification
- site privacy/security/legal → evidence-backed trust claims

Keep path instructions narrow enough to be relevant when loaded.

## Skills: reusable procedures

Skills answer *how to do a class of work well*. Organization-wide procedures live here under `skills/`; implementation-specific procedures stay in their owning repositories.

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

Repo-local skills currently include examples such as `repo-forensics`, `promise-product`, `promise-change-review`, `mail-platform-safety`, `ios-client-safety`, and `promise-marketing-copy`.

## Agents: durable company roles

Organization-level agents live under `agents/` so they can be used across Promise repositories.

- **Chief of Staff** — priorities, company review, open loops, risks, decision hygiene, and recurring operating work.
- **Product Critic** — product scope, UX coherence, feature pressure, positioning, and concept discipline.
- **Engineering Steward** — architecture, scale, complexity, state ownership, operability, and long-term technical shape.
- **PR Reviewer** — consequential implementation review across repositories.
- **Mail Platform Reviewer** — Gmail/Outlook integration, sync, identity, auth, mutation safety, reliability, and privacy.
- **Growth** — acquisition, messaging, experiments, funnel reasoning, and evidence-backed growth work.
- **Customer Operations** — support, customer signals, recurring confusion, retention/churn patterns, and feedback loops.
- **Trust Steward** — privacy, security, data handling, permissions, public claims, and trust-sensitive changes.
- **Finance & Operations** — vendor spend, cloud economics, recurring costs, operational leverage, and one-human-company sustainability.

Prefer a skill over a new agent unless a genuinely durable judgment role with distinct context and escalation behavior has emerged.

## Product truth agents should preserve

Promise is an AI-native, people-centric email client and memory layer. Its core jobs are:

- **I owe** — things the user said they would do
- **Waiting on** — things other people owe the user
- **Worth remembering** — useful details about people and relationships
- **Tell Promise** — private typed or spoken capture that becomes reviewable follow-up, action, or memory

The main surfaces are Today, Mail, People, Promises, and Tell Promise. New concepts should earn their way into this model instead of creating parallel task systems, generic AI dashboards, or extra inboxes to manage.

The person and open loop matter more than the thread. Provenance should travel with inferred information where available. Sending mail is explicit user action; remembering or creating a follow-up must never silently become a send.

## Architectural truth agents should preserve

- `UsePromise/platform` owns canonical backend business logic, data, provider integration, authorization, provenance, queues, schema, and production infrastructure.
- `UsePromise/ios` is a client. It consumes platform contracts and must not become a second source of backend truth.
- `UsePromise/site` owns acquisition, public product explanation, SEO, legal/support/security surfaces, and must not couple to platform internals.
- `UsePromise/promise-mcp` is an agent-facing client over the platform API. It must not bypass platform authorization, provenance, retention, or data boundaries.
- API/domain contracts flow outward from platform. Client repositories should consume generated or validated contracts rather than duplicate canonical business rules.

## Deterministic enforcement roadmap

When a rule can be tested mechanically, move it into CI rather than relying only on instructions. Candidate checks include:

- forbidden cross-repository/internal imports
- generated contract drift
- unscoped state/database access
- new dependency/service/queue/scheduled-job detection requiring a rationale
- public capability claims tied to a maintained capability inventory
- stale feature flags or compatibility paths
- migration and rollback checks

The target architecture is: **policy → always-on instruction → skill/agent reasoning → deterministic check where possible**.

## Evolution rule

Do not add another agent because a task feels specialized once. Add one only when a distinct judgment pattern recurs across work and cannot be represented cleanly as a skill used by an existing agent. Prefer adding or refining a skill first.
