# Promise Company OS

`UsePromise/company-os` is the executable coordination and observability layer for Promise's one-human-company operating model.

It exists because the organization now has enough independent agents, repositories, CI/governance loops, reviews, support/customer work, and recurring operations that founder coordination itself is becoming a system concern.

The repository should remain a **control plane above execution systems**, not another product backend.

## V0 role

V0 is intentionally observability-first:

- normalize GitHub PRs, issues, and workflow state into a common work graph
- show Needs You / In Progress / Waiting / Unowned / Blocked
- provide a stable registry of company agents/roles
- derive agent activity from owned work where possible
- preserve links/provenance to authoritative source systems
- expose a normalized snapshot for future integrations

It does not yet autonomously prioritize, assign, or execute discovered work.

## Relationship to the declarative operating system

`UsePromise/.github` remains the declarative company brain: principles, agents, skills, policies, and operating rituals.

`UsePromise/company-os` is the executable traffic-control layer: observation, normalized coordination state, future bounded orchestration, and founder-attention routing.

Repository/domain systems remain authoritative for execution and business truth.

## Evolution rule

Company OS may progressively automate coordination when the observed workflow is understood and the policy can be expressed with clear evidence, failure behavior, and escalation boundaries.

Agents may discover and propose work. Company OS should decide whether and when work enters the execution queue according to explicit policy rather than treating every signal as priority work.

The key outcome is the percentage of company operations that complete without requiring founder coordination while preserving quality, trust, and reversibility.
