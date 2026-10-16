# Production release gate: [release]

Artifact / source commit: [immutable identity]
Environment / configuration version: [values]
Scope / users / data affected: [values]
Assessment time / assessor / risk tier: [values and rationale]
Release authority / operator / monitoring owner: [roles]
Execution authorization: [present with scope/evidence, or pending]

> This records an assessment, not deployment permission. Replace fields and record real evidence. Use `PASS (executed)`, `FAIL (executed)`, `NOT RUN (reason)` or `NOT APPLICABLE (reason)`. Do not pre-check a row because a plan exists. Reassess affected rows when artifact or configuration changes.

## Evidence ledger

| Area | Applicable acceptance control | State | Exact command/method and evidence | Gap / risk / owner |
|---|---|---|---|---|
| Behavior | User acceptance, negative and edge cases | [state] | [result] | [gap] |
| Correctness | Invariants, transactions, concurrency, retry/duplicate effects | [state] | [result] | [gap] |
| Compatibility | Old/new binaries, clients, workers, events and contracts | [state] | [result] | [gap] |
| Access | Server authorization and tenant isolation | [state] | [result] | [gap] |
| Threats | Changed boundaries, abuse controls and negative tests | [state] | [result] | [gap] |
| Secrets/IAM | Scoped identities, rotation/configuration and no leakage | [state] | [result] | [gap] |
| Supply chain | Applicable dependency, secret, static, image/IaC checks | [state] | [result] | [gap] |
| Privacy | Sensitive storage/logs/traces, retention/deletion | [state] | [result] | [gap] |
| Migration | Mixed-version support, bounded backfill, reconciliation | [state] | [result] | [gap] |
| Recovery | Backup freshness, restoration/rehearsal, rollback limits | [state] | [result] | [gap] |
| Capacity | Representative latency, errors, workload and saturation | [state] | [result] | [gap] |
| Resilience | Deadlines/retries, backpressure, dependency failure | [state] | [result] | [gap] |
| Lifecycle | Startup/readiness, draining and graceful shutdown | [state] | [result] | [gap] |
| Observability | SLIs/SLOs, release visibility, routed alerts/runbooks | [state] | [result] | [gap] |
| Build/delivery | Immutable artifact, required CI/checks and provenance | [state] | [result] | [gap] |
| Handover | Docs/changelog, ownership and required communications | [state] | [result] | [gap] |

## Ordered rollout and observation

| Step | Action and prerequisites | Authorized owner | Success evidence | Abort trigger |
|---|---|---|---|---|
| [1] | [additive schema/config, compatible code, etc.] | [role] | [signal] | [condition] |
| [2] | [backfill, cutover, flag/canary exposure] | [role] | [signal] | [condition] |
| [3] | [monitoring and eventual cleanup] | [role] | [signal] | [condition] |

Observation window / dashboards / alert routing: [values and reason]
Affected external dependencies / communication plan: [values]

## Recovery procedure

Abort decision owner: [role]
Safe rollback command/procedure and prerequisites: [concrete steps]
Irreversible points / incompatible rollback states: [values]
Roll-forward / reconciliation / controlled replay: [concrete steps]
Recovery validation and RPO/RTO evidence: [values]

## Residual risks and exceptions

| Risk / failed or missing evidence | Impact | Compensating control | Authorized owner / acceptance evidence | Expiry / follow-up |
|---|---|---|---|---|
| [risk] | [consequence] | [control] | [role/record] | [trigger/date] |

## Gate decision

Recommendation: [GO / CONDITIONAL GO / NO-GO]
Rationale: [evidence and critical blockers/conditions]
Required sign-offs: [actual state, not inferred approval]

`GO` needs applicable evidence and acceptable authorized residual risk. `CONDITIONAL GO` needs owned, accepted noncritical gaps and controls. A critical failed/uncertain invariant, access boundary, recovery requirement or missing execution authority requires `NO-GO` for execution. An agent cannot approve its own exception.

## Execution record, if authorized and performed

[Actual artifact/environment, timestamped actions, observed user/data results, abort/recovery actions and pending follow-ups. If no deployment occurred, state that explicitly.]
