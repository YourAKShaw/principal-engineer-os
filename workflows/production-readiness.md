# Production readiness and release gate

Use for a launch assessment, release decision or operating handover. Assessing readiness does not authorize deployment. Existing deployment authorization may be sufficient; do not ask again solely because this workflow is used.

Read the constitution plus references for changed security/data/operational boundaries. Use [the production gate](../assets/production-gate.md) to record evidence for one exact artifact, environment and release scope.

## Gather evidence, not checkmarks

Identify source commit/artifact, configuration, affected users/data, risk tier, acceptance criteria, approver/operator, release window and observability. Inspect actual CI/results, contracts, migrations, runbooks and environment constraints. Distinguish absent evidence from confirmed failure. If the artifact/config changes after assessment, re-evaluate affected evidence.

Assess applicable controls:

- **Behavior:** acceptance/negative cases, business invariants, concurrency and retry semantics, compatibility with clients/jobs/old binaries.
- **Security/privacy:** changed threat boundaries, server permissions/tenant isolation, secrets/IAM, relevant scans, sensitive storage/telemetry/retention.
- **Data:** mixed-version schema support, rehearsed bounded backfill, reconciliation, backup/restore, irreversible points and forward repair.
- **Reliability/performance:** meaningful capacity evidence, limits/deadlines/retries, readiness/shutdown, dependency failure, SLOs, actionable alerts and runbooks.
- **Delivery:** immutable traceable artifact, executed required checks, ordered migrations/config, progressive release, owner, monitoring window, abort criteria and usable recovery procedure.

Mark nonapplicable controls with reasons. Do not require every production mechanism for a small library release, or waive a critical permission boundary because a diff is small.

## Define the executable transition

Order additive schema/config changes, compatible code, backfill/cutover, flags and eventual cleanup. Verify old consumers and workers can coexist. Name who performs each consequential step and who observes user/data signals.

Specify canary/flag exposure where useful, smoke checks and observation duration from the risk/failure model. Set concrete abort triggers and recovery commands/procedure with prerequisites. After irreversible transformations, an old binary or destructive down migration may not be safe; supply forward recovery.

If deployment is authorized, stay within the exact scope and permissions, inspect the concrete plan and stop on failed gates or abort signals. Do not bypass protected checks or self-approve an exception. Missing approval should leave a reviewable artifact and clear pending action, not unfinished preparation.

## Gate decision and handoff

- **GO:** applicable evidence is present and residual risk is acceptable under the authorized policy.
- **CONDITIONAL GO:** noncritical residual risks have authorized owners, compensating controls and follow-up conditions; identify who can accept them.
- **NO-GO:** a critical invariant, access boundary or recovery requirement remains failed or materially uncertain, or required authority is absent.

An assessment recommendation is not a self-issued exception or deployment permission. Critical missing evidence cannot become green through a checklist label. If execution was authorized, report the actual deployed artifact, observed results and any recovery actions. Otherwise report the gate status, blockers/conditions and prepared next action without implying deployment occurred.
