# Design a system

Use for a new system, major integration or expensive architecture decision. Produce a design unless implementation is also authorized. Scale the depth to the decision; do not turn a small design question into a full RFC.

Read the constitution and the architecture reference. Add APIs/data, security, reliability or AI guidance only for affected boundaries.

## Discover the actual problem

Identify users, actors, capabilities, journeys and success criteria. Separate functional needs, quality attributes and non-goals. Inspect the existing system before proposing its replacement.

Record material constraints as known, estimated or unknown: workload/peaks, data size/growth, read/write mix, latency, consistency, availability, RPO/RTO, team/ownership, budget, deadline, hosting, privacy/residency and migration tolerance. Ask about unknowns that change an expensive choice; use labeled reversible assumptions otherwise. Assign the risk tier.

Turn critical requirements into observable contracts. For example, a retry after a payment-provider timeout must expose a pending/reconcilable outcome and must not issue a new charge merely because the first request timed out.

## Model boundaries and alternatives

1. Identify bounded contexts, sources of truth, aggregate/state-machine invariants, tenant/access boundaries and atomic transactions.
2. Sketch actors/external systems, deployable units/stores and critical request/event sequences. Label trust, consistency and ownership boundaries.
3. Define API/event semantics, IDs, idempotency, errors and compatibility for important paths.
4. Compare credible options for consequential choices, including a minimal viable baseline. State the decisive drivers and costs: complexity, correctness, operations, performance, deployment autonomy, vendor dependence, total cost and migration.
5. Select a reversible path with evidence or an explicit validation experiment. Record expensive choices in an ADR and identify observations that would invalidate them.

Start from a modular application where appropriate. A service boundary requires more than a folder name or hypothetical future scale.

## Walk through failure and evolution

Trace a normal operation, then applicable timeout, duplicate, partial commit, stale cache, unavailable database/queue/provider, overload, revoked permission and regional failure cases. Explain user-visible state and how the system detects and repairs uncertainty.

Define resource bounds, time/retry budgets, telemetry, SLOs, ownership, backups and restoration. Show rollout, old/new compatibility, rollback limits and forward recovery. Cost estimates need units, assumptions and sensitivity, not fabricated precision.

Describe the next cheapest evolution step and its trigger, such as measured DB saturation or independent release ownership. Deferred features are not present capabilities.

## Deliver and validate the proposal

Use [the RFC template](../assets/system-design-rfc.md) for substantial designs and [the ADR template](../assets/adr-template.md) for focused decisions. Include the selected architecture and why, constraints/unknowns, boundaries/data/flows, alternatives, critical failure/security behavior, capacity/cost assumptions, operational plan, milestones and acceptance methods.

If runtime tools are unavailable, offer a verification plan rather than invented benchmarks. Confirm that another engineer can implement incrementally without relying on unspoken state or permissions.

**Completion:** the decision is understandable and proportional; critical invariants, trust and failure boundaries are explicit; meaningful alternatives were assessed; uncertainty has an owner or validation path; an executable implementation/acceptance plan exists. Do not claim implementation or production readiness from a design alone.
