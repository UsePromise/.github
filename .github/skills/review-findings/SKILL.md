---
name: review-findings
description: Turn code-review findings into inline, evidence-backed, fix-first GitHub review comments with concrete suggested patches where safe.
---

# Review findings

Use this skill whenever an agent or skill discovers a code-local issue in a pull request.

## Default behavior

Prefer **inline + fix-first** over a detached audit report.

If the finding can be anchored to a changed line or hunk:

1. attach it to the narrowest relevant diff location
2. state the concrete defect or unsafe assumption
3. explain the realistic failure mode or user/system impact
4. propose the smallest safe correction
5. include a GitHub `suggestion` block when the replacement is local, unambiguous, and safe to apply directly

Use a top-level PR finding only when the concern is genuinely cross-cutting: architecture, missing migration/rollback plan, product-scope drift, contract strategy, missing end-to-end validation, or a problem spanning multiple files where one inline location would mislead.

## Finding contract

Each material finding should be representable as:

- `path` — repository-relative file path when code-local
- `line` — right-side diff line when code-local
- `side` — normally `RIGHT`
- `severity` — `blocking`, `high`, `medium`, or `low`
- `title` — concise defect statement
- `rationale` — why the issue is real and consequential
- `evidence` — concrete execution path, contract, test, or invariant
- `suggestedFix` — specific correction, not generic advice
- `suggestedPatch` — exact replacement text when safely auto-applicable
- `canAutoApply` — true only when the patch is local, complete, and does not require hidden judgment

Do not invent a line anchor merely to make a comment inline. If the defect is in unchanged code exposed by the PR, anchor to the changed call site when that is a truthful place to explain the problem; otherwise use a top-level finding with explicit file/function evidence.

## Comment shape

Keep inline comments short enough to act on immediately:

**[severity] Title**

Why this matters: <concrete failure mode>.

Suggested fix: <smallest safe correction>.

When safe, follow with a fenced `suggestion` block containing only the replacement lines.

## Fix quality

A proposed fix must preserve the repository's architecture and product invariants. Do not recommend a local patch that merely hides a deeper state-ownership, auth, retry, provenance, or contract bug.

If multiple valid fixes exist and product/architecture judgment is required, propose the decision and alternatives rather than presenting one patch as mechanically correct.

## Review summary

After inline findings are emitted, the top-level review should summarize only:

- blocking findings
- cross-cutting concerns
- validation gaps
- whether the PR is otherwise clear to proceed

Do not duplicate every inline comment in the summary.