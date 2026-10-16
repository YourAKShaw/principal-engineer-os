# Refactor, debug and optimize

Choose the branch that matches the user request. A refactor preserves observable behavior; a bug fix deliberately changes it; an optimization needs comparable measurement. Do not mix unrelated cleanup into diagnosis.

## Debug: establish cause before changing scope

1. Define the symptom, expected behavior, environment/version, affected users and timing. Inspect code, logs, traces and recent relevant changes; protect sensitive data.
2. Reproduce safely or capture the closest observable evidence. Rank hypotheses by supporting and contradicting evidence. Do not equate the latest commit with root cause without a causal path.
3. Narrow the fault using targeted tests, read-only probes and controlled experiments. Bound effects; avoid blind restarts or production mutations that destroy evidence.
4. Identify the broken invariant and cause. Implement the smallest correct fix within authorization, with appropriate failure/compatibility handling.
5. Add a regression check that distinguishes old/new behavior when practical. Run relevant checks and inspect adjacent paths likely to share the cause.
6. Report confirmed root cause separately from remaining hypotheses, the fix, actual evidence and any monitoring/recovery needs.

If no reproduction/runtime access is available, continue useful code/evidence analysis and give a ranked diagnostic plan. Do not pretend the cause is proven. Active outages should also use the incident workflow.

## Refactor: prove preservation

Identify the specific maintenance problem and intended benefit: reduced coupling, removed duplication of an invariant, clearer state ownership or cheaper change. Inspect public entry points, callers, serialization, persistence and error behavior before editing.

Establish characterization evidence before the move. Preserve observable output, side effects, ordering, errors, concurrency semantics and contracts; do not assume names document behavior. If existing behavior is unsafe, separate the proposed correction from the preservation claim.

Work in small coherent slices. Add abstractions only when they eliminate real complexity or enforce a boundary. Delete obsolete paths after checking consumers; update docs/config and maintain a safe migration path for stateful changes. Run relevant regression and performance checks. Read the APIs/data reference for large stateful refactors.

Red flags: unrelated mass churn, new indirection without simpler reasoning, cycles, mocked-away integration behavior, hidden behavior changes, or parity claims without evidence.

## Performance: measure end-to-end value

Read reliability/observability/performance guidance. Define the workload and acceptance metric, record a baseline and environment, profile the actual bottleneck, change the smallest meaningful cause and compare under equivalent conditions. Check p95/p99, errors, resource saturation and cost, not just an isolated mean.

Use representative data, cache states, concurrency and repeated runs to expose noise. Avoid uncontrolled production or provider load. Do not fabricate speedups or infer them from algorithmic intuition alone. Without runtime evidence, deliver an instrumentation/benchmark plan and state that performance remains unverified.

## Completion

The diagnosis is supported by evidence, the requested behavior or preservation goal is checked, unrelated scope is avoided and remaining uncertainty is explicit. Report commands/methods actually used and limitations. A refactor that changes behavior must identify that change; an optimization without measurements must not claim a measured gain.
