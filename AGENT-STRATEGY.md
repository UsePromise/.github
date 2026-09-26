# Promise agent strategy

Promise should use a small number of durable specialist agents backed by reusable skills. The goal is not to create a persona for every task. The goal is to make high-value judgment repeatable while keeping implementation knowledge close to the repositories that own it.

## The model

### 1. Repository instructions: always-on local truth

Each repository owns a concise `AGENTS.md` (and, where useful, Copilot instructions) describing:

- what the repository owns
- what it must not own
- authoritative architecture and product docs
- critical invariants
- the smallest correct validation commands

These instructions should stay short enough to be useful on every task.

### 2. Skills: reusable procedures

Detailed methods belong in `.github/skills/<skill>/SKILL.md` inside the repository where the procedure is relevant. Skills should answer *how to do a class of work well*, not impersonate a role.

Examples in the Promise repos include:

- `repo-forensics`: reconstruct a system before making architectural judgments
- `promise-product`: test a change against Promise's product model and vocabulary
- `promise-change-review`: perform evidence-first, risk-weighted change review
- `mail-platform-safety`: reason about provider sync, identity, retries, mutations, and mail capability gates
- `ios-client-safety`: protect account isolation, API-contract, cache, and native UX invariants
- `promise-marketing-copy`: keep public claims concrete, human, differentiated, and supportable by the shipped product

### 3. Custom agents: a small set of durable viewpoints

Organization-level agents live in this repository under `agents/` so they can be used across Promise repositories.

| Agent | Use it for | Do not use it as |
| --- | --- | --- |
| `promise-product-critic` | Product/UX proposals, feature scope, product copy, deciding whether something belongs in Promise | A generic feature generator |
| `promise-pr-reviewer` | Consequential implementation review across platform, iOS, site, and future clients | A lint bot or style reviewer |
| `mail-platform-reviewer` | Gmail/Outlook integration, sync, auth, mailbox actions, sending, identity, reliability, privacy | A general-purpose backend engineer |

Agents should load and obey repository-local instructions and skills before applying their own viewpoint.

## Product truth agents should preserve

Promise is an AI-native, people-centric email client and memory layer. Its core jobs are:

- **I owe** — things the user said they would do
- **Waiting on** — things other people owe the user
- **Worth remembering** — useful details about people and relationships
- **Tell Promise** — private typed or spoken capture that becomes reviewable follow-up, action, or memory

The product should make the person and the open loop more important than the inbox thread. When Promise infers something from source material, provenance should travel with the result where available. Sending mail is an explicit user action; remembering or creating a follow-up must never silently become a send.

The main product surfaces are Today, Mail, People, Promises, and Tell Promise. New concepts should earn their way into this model instead of creating parallel task systems, generic AI dashboards, or extra inboxes to manage.

## Architectural truth agents should preserve

- `UsePromise/platform` owns canonical backend business logic, data, provider integration, authorization, provenance, queues, schema, and production infrastructure.
- `UsePromise/ios` is a client. It consumes platform contracts and must not become a second source of backend truth.
- `UsePromise/site` owns acquisition, public product explanation, SEO, legal/support/security surfaces, and must not couple to platform internals.
- `UsePromise/promise-mcp` is an agent-facing client over the platform API. It must not bypass platform authorization, provenance, retention, or data boundaries.
- API/domain contracts flow outward from platform. Client repositories should consume generated or validated contracts rather than duplicate canonical business rules.

## Review philosophy

Agents should optimize for consequential correctness, not the number of comments. A useful review finds the few issues that can cause wrong-account data, incorrect provider mutations, lost provenance, contract drift, misleading product behavior, unsafe retries, hidden capability mismatches, or hard-to-debug production failure.

Prefer evidence from implementation, tests, contracts, and runtime configuration over comments or assumptions. Prefer the smallest validation that proves the change. When behavior is intentionally gated, do not infer that deployed code means enabled product behavior.

## Evolution rule

Do not add another custom agent because a task feels specialized once. Add one only when a distinct judgment pattern recurs across changes and cannot be represented cleanly as a skill used by an existing agent. Prefer adding or refining a skill first.
