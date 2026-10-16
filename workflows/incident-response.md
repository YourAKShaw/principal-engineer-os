# Incident response and emergency diagnosis

Use for an active outage, degradation, suspected compromise or data-integrity incident. Read the constitution and relevant operational/security/data references. Prioritize user safety and reversible containment over a broad rewrite.

## Triage and establish control

Record confirmed impact, start/detection time with timezone, affected journeys/tenants/regions, data/secret risk and ongoing blast radius. Identify the responsible owner and severity using the team's definitions. Separate incident coordination from technical investigation when staffing permits.

Preserve a timestamped timeline, release/config versions, relevant protected logs/traces and actions/results. Minimize sensitive content in incident notes. Use existing authorized communication routes; drafting a status does not authorize sending it externally.

## Stabilize within authority

Choose a reversible mitigation supported by evidence: reduce traffic, disable a flag, roll back compatible code, isolate a dependency or pause a harmful worker. Confirm scope, compatibility, recovery preconditions and authorization before executing. Prior approval remains valid for the authorized action; the incident itself does not create new access rights.

Do not blindly restart components, delete queues/data, weaken access controls, replay non-idempotent effects or run a destructive down migration. A timeout can conceal a completed charge/write. If authority or safety evidence is missing, prepare the concrete action and identify the required owner while continuing safe diagnosis.

## Investigate and recover

1. Correlate recent releases/config, dependency health, SLO burn, logs/traces, DB/pool/queue metrics and saturation. Avoid anchoring on the latest change alone.
2. Rank hypotheses by evidence; distinguish root cause from secondary symptoms.
3. Use targeted bounded probes or experiments. Preserve evidence and avoid exposing customer data in commands/output.
4. Apply the smallest safe fix or continue containment. Reconcile uncertain/partial effects; use controlled resumable replay with deduplication and quotas.
5. Restore gradually, verifying user outcomes and data integrity, not only process health. Watch backlog/retry storms and avoid saturating a recovering dependency.

Stop an action when its abort criteria fire or effects exceed the authorized scope; do not repeat expensive or irreversible steps just because tool feedback is missing. Record what happened and move to the defined recovery/escalation path.

## Communicate and learn

Prepare concise updates: confirmed impact, mitigations/actions, observed recovery, remaining uncertainty and next update checkpoint. Never conceal impact or present a hypothesis as proven. Send only through explicitly authorized channels.

After stabilization, capture a blameless timeline, contributing factors, detection/recovery gaps and customer/data impact. Assign follow-ups with owners, priorities, due dates and verification criteria; reconcile emergency configuration into source control. Add regression, alerting or recovery rehearsal where it prevents the demonstrated failure.

**Completion:** the service and data are stable under observed conditions, uncertain effects are reconciled or explicitly owned, recovery is documented, and follow-ups are assigned. If recovery could not be performed, report the current impact and exact blocker; do not claim resolution from a proposed mitigation.
