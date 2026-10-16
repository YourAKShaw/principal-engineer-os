# System design RFC: [system / capability]

Status: [draft / in review / accepted / superseded]
Date / owner / reviewers: [values]
Requested artifact / authorization: [design only, or precise implementation scope]
Risk tier: [R0–R4 and reason]

> Adapt to the decision's scale. Replace bracketed fields, label estimates/unknowns, remove inapplicable sections with reasons. Planned controls and tests are not implemented or executed evidence.

## 1. Decision and user outcome

[Problem, selected approach and why it solves the actual job. Summary of the consequential trade-off.]

## 2. Requirements and non-goals

Actors / journeys: [values]
Capabilities and acceptance criteria: [testable outcomes]
Non-goals / deferred work: [values]

## 3. Constraints and assumptions

| Input | Known / estimated / unknown | Value, source and effect if wrong |
|---|---|---|
| Team, ownership, deadline, budget | [state] | [constraints] |
| Existing runtime/hosting/data | [state] | [versions and current system] |
| Privacy, residency, legal obligations | [state] | [applicable scope and qualified input] |
| Consistency, availability, latency, RPO/RTO | [state] | [targets, windows and workload] |

Material questions / owners: [what blocks an expensive decision]

## 4. Workload, capacity and cost

[Normal/peak arrivals, concurrency, payload, read/write mix, dataset/index size, retention/growth, background work and egress. Show units, assumptions and sensitivity; distinguish modeled from measured. Include operator and telemetry cost.]

## 5. Boundaries and flows

[Context diagram, deployable/store view and critical sequences as useful. Label actors, trust/tenant boundaries, owners, protocols and sources of truth. Include failure and async flows, not only the happy path.]

## 6. Domain, state and data

[Entities, state transitions, atomic invariants, transaction/isolation boundaries, dedupe identity, concurrency, authoritative state and eventual-consistency points. Lifecycle, retention/deletion and export.]

## 7. Interfaces and evolution

[API/event schemas, permissions, errors, pagination, idempotency, ordering/replay, quotas, external integration semantics, compatibility/deprecation and old/new consumer coexistence.]

## 8. Alternatives and selected architecture

| Option | Correctness/security | Complexity/operability | Performance/cost | Migration/reversibility |
|---|---|---|---|---|
| [minimal viable baseline] | [trade-off] | [trade-off] | [assumptions/evidence] | [path] |
| [credible alternative] | [trade-off] | [trade-off] | [assumptions/evidence] | [path] |

[Selection and decisive drivers; link important ADRs. Avoid arbitrary scoring.]

## 9. Threat model and privacy

[Assets, actors, entry points and trust boundaries; material threats, enforcement points, negative tests, residual risks/owners. Secret/provider/data-governance requirements and relevant compliance evidence, without claiming certification.]

## 10. Failure, overload and recovery

| Scenario | User-visible state / invariant | Detection and containment | Recovery / owner |
|---|---|---|---|
| [timeout, duplicate or partial success] | [semantics] | [signals and limits] | [reconcile or retry policy] |
| [dependency failure or saturation] | [degraded behavior] | [deadlines, backpressure] | [restore/failover path] |
| [bad deploy or data issue] | [semantics] | [abort trigger] | [rollback/forward repair] |

[Backups, restore evidence, RPO/RTO and failure-domain dependencies.]

## 11. Operations and delivery

[SLIs/SLO windows, logs/metrics/traces and sensitive-data controls, alerts/runbooks, on-call owner, configuration/secrets, CI/artifact, rollout exposure and observation window. Migration order, recovery prerequisites, irreversible points and retirement. Identify authority needed before execution.]

## 12. Milestones and acceptance

| Slice | Owner / dependencies | Observable acceptance | Verification / evidence state |
|---|---|---|---|
| [first complete vertical slice] | [values] | [behavior] | [planned or executed method] |
| [subsequent milestone] | [values] | [behavior] | [planned or executed method] |

## 13. Risks, unknowns and evolution

[Prioritized risks with controls/owners; missing evidence; decision falsifiers; measured scaling/revisit triggers and next cheapest evolution step. Record required sign-off separately from design acceptance.]
