---
name: public-claim-verification
description: Verify website, App Store, investor, launch, pricing, privacy, security, and product claims against current implementation and rollout state.
---

# Public Claim Verification

For every material public claim, find current evidence in code, configuration, product behavior, policy, or authoritative documentation.

Pay special attention to:
- provider parity and capability flags
- AI behavior and limits
- retention/history claims
- privacy/security/training claims
- pricing and paid capability
- notifications/background behavior
- sending or autonomous-action language
- platform availability

Classify claims as `supported`, `qualified`, `not yet supported`, or `cannot verify`.

Prefer narrow truthful wording over aspirational present tense. A coded feature behind disabled flags is not automatically a shipped capability. Never infer legal/security assurances from architecture alone.

## Output

Return the claim, evidence, qualification required, and replacement wording where needed. Highlight contradictions across site, product UI, FAQ, App Store copy, and docs.
