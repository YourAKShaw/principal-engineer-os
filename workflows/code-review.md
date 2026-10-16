# Review, audit and debt triage

Use for diff review, codebase assessment, security review or architecture audit. Review produces findings; do not modify files unless fixes are authorized. Load domain references for the boundaries actually under review.

## Establish the review surface

Inspect the requested diff/revision or system scope, user goal, repository policies, related callers/tests/contracts and operating constraints. Understand current behavior before evaluating it. Mark missing evidence, especially absent traffic, incident history or deployed configuration. A risky possibility is not automatically a confirmed defect.

Prioritize correctness/business invariants, access/tenant/privacy, data/concurrency, compatibility/migrations, operational failures, performance, maintainability/testing, then style. Do not let many low-value nits bury a release-blocking authorization error.

Trace relevant normal and adverse paths: untrusted input to its sink, identity to object lookup, state transition to commit, external effect to reconciliation, and error to user/operator. Look beyond the edited line for jobs, caches and older consumers. Use focused read-only checks where feasible; do not run unsafe project code or exploit a live service without authority.

## Report actionable findings

Each finding should name severity/confidence, exact location when known, concrete trigger, observable impact, evidence/reproduction, a minimal remediation and relevant test gap. Confirm that the changed code causes the issue for diff review; do not present pre-existing defects as newly introduced.

Severity is contextual:

| Level | Meaning |
|---|---|
| P0 | Active catastrophic/security or data-destructive issue requiring immediate response |
| P1 | Serious correctness/security/reliability defect that blocks release |
| P2 | Important defect or significant demonstrated operating risk |
| P3 | Noncritical maintainability/performance problem |
| Suggestion | Optional improvement without a release-blocking claim |

Example shape: `[P1, high confidence] Cross-tenant invoice disclosure at <verified location>: authenticated tenant A can supply B's invoice ID because lookup omits authorized tenant scope. Evidence: <inspected query or safe reproduction>. Fix: scope by trusted tenant at access boundary and add a negative test.` Replace placeholders with actual evidence; do not fabricate line numbers or reproduction results.

Keep confirmed findings separate from hypotheses and optional recommendations. If no actionable defect was established, say so and identify material verification limits; do not invent findings to fill a quota. A review is not a guarantee of absence of defects.

## Architecture audit branch

Map modules/services, deployables, dependencies, data owners and critical journeys. Review:

- Invariant ownership, duplicated/contradictory policy and boundary violations.
- Identity and authorization including async/admin/export paths.
- Datastore consistency, query hotspots and migration/recovery safety.
- Latency, capacity, cache correctness and distributed call chains against actual evidence.
- Test signal/flakiness, dependency/supply-chain risk and CI privileges.
- SLOs, alerts, runbooks, restore evidence and operational ownership.

Classify confirmed issues separately from unverified hypotheses. Rank remediation by impact, likelihood, effort, dependencies and owner; avoid arbitrary numerical precision. Propose immediate fixes, medium-term capabilities and optional strategic evolution. Track conscious debt with its ongoing cost and revisit trigger.

For a requested security assessment, add a focused threat model, attacker preconditions and control verification. Do not label scanner output alone a confirmed exploit or call the system compliant.

## Completion

Lead with the most consequential findings, then assumptions and verification limits. For an audit, include a compact system map, prioritized remediation plan and success criteria. Preserve the distinction between review, approved remediation and deployment.
