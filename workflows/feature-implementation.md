# Implement a feature or fix

Use for a ticket, API/UI change, worker, integration, bug fix or migration. For a tiny change use only the relevant steps. For diagnosis-first work, also use the debug workflow.

## Inspect and define the behavioral change

Read project instructions, working-tree status, related implementation/tests, callers, runtime/dependency versions, data model and contracts. Identify current entry points, state owners and external effects. Preserve user edits. Reproduce the bug if feasible before choosing a fix.

Define actor, valid input, permission/tenant scope, invariant, transition and observable output. Include material negative cases, compatibility, concurrency, retries and partial failures. Use existing acceptance criteria; do not silently add features. Classify risk and read references for affected boundaries.

Make a concise implementation plan for substantial work. Use an ADR only for a consequential choice. Prefer a coherent vertical slice and safe nearby conventions over broad rewrites.

## Implement and verify the boundary

Implement domain rules and runtime parsing, relevant authorization, persistence/transactions, transport, external effects and diagnostics. Keep errors safe and useful. Bound resource use and define cancellation/cleanup for async work. Add dependencies only for a justified need.

Test at the layer where the changed invariant can fail. Relevant cases may include invalid input, unauthorized/not-found/conflict, tenant crossover, competing writes, duplicate requests, timeout after success, stale state and provider failure. Do not create a full matrix of irrelevant cases. Use real integration checks where mocks would conceal the risky semantics.

For a bug, ensure a meaningful regression check fails on the original behavior and passes with the fix when practical. Run focused checks, then impacted broader checks. Disclose pre-existing failures and missing tools; do not weaken controls to hide them.

Update affected API/config/examples, docs and runbooks. Inspect the final diff for unrelated churn, secrets, accidental compatibility breaks and changes to user work.

## Migration and stateful refactor branch

Read the APIs/data migration guidance. A migration is not complete after only a schema edit:

1. Inventory all old/new readers and writers, including jobs and long-lived clients; quantify data, lock/disk and replica impact.
2. Define expand, dual compatibility/shadow, bounded backfill, reconciliation, cutover, monitoring and eventual contract/retirement stages.
3. Make batches idempotent, resumable and rate-limited with stable cursors and progress/error signals. Handle writes during backfill.
4. Rehearse high-risk volume/concurrency and recovery; identify irreversible points, abort triggers and authorized owner.
5. Verify mixed-version operation, preserved invariants and repaired drift before switching authority or removing old structures.

Preparation does not authorize production migration execution. State precisely what is implemented, rehearsed or merely planned.

## Complete the change

Check acceptance behavior, changed trust/data boundaries, failure paths, actual test evidence and compatibility. Note rollout flags/order, monitoring and recovery where risk warrants them. If production readiness is requested, also use the release workflow.

Report delivered behavior and relevant files, key decisions, exact checks/results, migrations/breaking changes, known risks and deployment state. Do not call unexecuted behavior verified or a locally passing feature production-ready without the applicable operating evidence.
