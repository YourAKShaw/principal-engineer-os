# Reliability, observability and performance

Use for operational behavior, SLOs, failures, capacity or measured optimization. Contents: service levels; failure controls; recovery; signals; measurement; scaling/cost.

## Define user-centered success

Choose SLIs for actual journeys: successful checkout, durable write, response latency, notification freshness. Define the SLO's numerator, denominator, window, workload and exclusions; distinguish an internal objective from a contractual SLA. Process uptime alone does not prove user success. Do not promise availability percentages without a dependency model, operating budget and measurement.

For binary continuous availability, a 99.9% SLO in a 30-day month allows approximately 43.2 minutes of failed-service-equivalent time: `(1 - SLO) × minutes`. Request-based accounting can differ. Use error budgets and burn rates to make delivery/reliability trade-offs explicit rather than treating 100% as a free target.

## Walk the failure path

For critical flows assess dependency timeouts/partial outages, DNS, network partitions, throttling, connection pool exhaustion, disk full, CPU/memory saturation, expired certificates, queue lag, bad deploys, version mismatch, operator error, corruption and malicious load. For each material case define detection, containment, degraded semantics, recovery and owner.

Use end-to-end deadlines, propagated cancellation, bounded resources, eligible retries with jitter, retry budgets, circuit breakers and bulkheads as needed. Avoid multiplying retries at multiple layers. Set queue/concurrency limits and admission or load-shedding behavior before overload becomes an outage. Never return fake success after swallowing an exception.

Liveness asks whether a process can make progress; readiness asks whether it can serve its intended traffic. Dependency unavailability does not always justify restarting a healthy process. Specify startup, health probes, signal handling, draining and what happens to in-flight requests/jobs during shutdown.

## Recovery is a tested capability

Define RPO/RTO, critical data/assets, failure domains, backup/replication policy, access/credential dependencies and recovery order. Track backup freshness and isolation; rehearse clean restoration and time it. Replication is not a backup against all corruption or deletion. A failover claim requires an implemented, tested data and traffic strategy.

Keep runbooks with actionable detection, safe diagnostic commands, mitigation/recovery steps, prerequisites, abort criteria, escalation and ownership. During incidents preserve evidence and stabilize users before deep diagnosis. Separate coordination from investigation when staffing permits. Postmortems should track contributing factors, detection gaps and owned follow-ups without blame.

## Instrument for questions operators must answer

| Signal | Baseline | Guardrail |
|---|---|---|
| Logs | Timestamp, severity, service/version/environment, operation, safe code, request/trace context | No secrets, sensitive raw payloads or duplicate exception spam |
| Metrics | Traffic, errors, latency histograms, saturation, pools, dependency failures, job lag/retry/DLQ, business outcomes | Bound label cardinality; no raw user/request IDs or arbitrary messages |
| Traces | Entry/dependency spans, async context, release attributes, trace/log correlation | Safe attributes, deliberate sampling and retention |
| Profiles | CPU/heap/allocation evidence for hot paths | Bound overhead and sensitive capture |
| Alerts | User-impact or impending-exhaustion conditions | Actionable, deduplicated, routed to an owner and runbook |

Dashboards should expose critical journeys, golden signals, dependencies, release and region, plus SLO burn where available. Prefer OpenTelemetry-compatible signals when appropriate to the stack. Decide retention, access, sampling and telemetry cost. A failed telemetry backend must not take down the application.

For a critical new flow, demonstrate how an operator detects failure, distinguishes access/dependency/capacity/data problems, identifies the responsible release and recovers. Logging every payload is not observability.

## Performance investigation protocol

1. Define the symptom and success criterion under a representative workload: p95/p99, achieved throughput, error rate, memory, freshness or unit cost.
2. Capture a reproducible baseline with environment, versions, dataset/cardinality, limits, concurrency, request mix and warm/cold cache conditions. Repeat sufficiently to reveal variability; label confidence and gaps honestly.
3. Decompose service/queue/network/DB/external-call/serialization/rendering time. Profile the measured bottleneck. Amdahl's law limits the end-to-end value of optimizing a minor component.
4. Change the smallest meaningful cause: algorithm, N+1, query/index, payload, round trips, pool sizing or allocation before adding infrastructure.
5. Repeat comparable measurement; inspect correctness, tail latency, errors, resource use and cost. Report regressions and trade-offs, not only a best-case number.

If the runtime or representative data is unavailable, produce an instrumentation/benchmark plan and disclose the gap. Code inspection does not establish a speedup.

## Match scaling to the bottleneck

| Bottleneck | First investigation | Escalate after evidence |
|---|---|---|
| CPU | Profiles, repeated work, algorithmic cost | Horizontal/parallel compute |
| Database | Plans, indexes, batching, transactions, pool use | Replicas, partitioning, workload separation |
| Memory | Heap growth, leaks, unbounded collections/cache | Instance sizing and workload isolation |
| Network | Round trips, payload, compression | CDN, regional placement, protocol change |
| External provider | Deadlines, quota, batching, safe caching | Async path or fallback provider |
| Worker lag | Handler costs, concurrency, hot keys | Partition consumers and isolate workloads |
| Browser | Bundle, image, render and fetch waterfall | SSR, preload or edge when justified |

For IO-bound work use appropriate asynchronous IO; CPU-bound work needs bounded execution resources. Guard event loops, tasks/goroutines/promises, connection lifetimes, deadlocks and cleanup. Cancellation and shutdown behavior are part of performance under load.

Load-test steady, ramp, burst, peak, soak and failure conditions proportionate to risk. Include realistic authentication, tenant skew, data size and think time; distinguish offered from achieved load. Report latency distribution, errors, saturation, queue depth and pool/CPU/memory. Do not stress production or third parties beyond authorization.

Track total cost per useful outcome, not just instance price: egress, replicas, backups, telemetry, staging and operator time count. Set budget alerts and scaling limits. Avoid wasteful polling/computation; assess energy impact where material.

## Foundations

[Google SRE](https://sre.google/sre-book/table-of-contents/), [SRE Workbook](https://sre.google/workbook/table-of-contents/), [OpenTelemetry](https://opentelemetry.io/docs/), [Prometheus practices](https://prometheus.io/docs/practices/). Adapted from master §§15–17, 25 and 31. Verify instrumentation semantics for installed versions.
