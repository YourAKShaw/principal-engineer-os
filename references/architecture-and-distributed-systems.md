# Architecture and distributed systems

Use for system boundaries, capacity, distributed coordination, queues or caches. Contents: selection; workload; consistency; failure semantics; building blocks; scenario defaults.

## Select boundaries before infrastructure

Map actors, external systems, bounded contexts, owners, critical journeys, data sources of truth and atomic invariants. Sketch context, deployable-unit and critical sequence views where they expose a decision; C4 is a useful vocabulary, not a mandatory drawing exercise.

Start with a modular monolith when it fits. Organize around capabilities with deliberate public contracts and controlled data ownership. A small CLI need not imitate domain/application/infrastructure folders. Clean, hexagonal or onion architecture helps when stable policy must survive multiple transports or infrastructure changes; use only the indirection that isolates actual variation.

Use DDD to find language, aggregates and contexts with domain experts. Aggregate boundaries follow atomic invariants, not database tables. Straightforward CRUD need not become an elaborate domain model.

Independent services need a benefit such as scaling, release autonomy, compliance isolation or ownership. Budget for service authentication, owned data, contracts, tracing, routing, partial failures, deployment, on-call and distributed consistency. Lockstep releases plus shared uncontrolled writes indicate a distributed monolith; recombination may be cheaper.

Serverless suits bounded, bursty managed execution but has runtime limits and cold-start/diagnostic costs. Batch favors throughput with checkpoints. Streaming requires ordering, windows, watermarks and replay semantics. Edge execution changes locality, state and runtime constraints. Choose from workload and operational capacity.

## Capacity assumptions and service properties

Record normal and peak arrival rates, distribution, concurrency, payload size, read/write ratio, retention, storage/index growth, egress, background work and team budget. Label estimates and use units. Derive peaks from a stated traffic model rather than presenting a daily average as capacity.

For a stable system, Little's law `L = λ × W` relates average in-flight work, arrival rate and mean response time. It does not eliminate burst or saturation analysis. Separate service time from queueing and end-to-end latency. Define latency percentiles and error targets under a named workload and environment.

Specify properties per operation: consistency (including read-your-writes), durability of an acknowledgment, availability from user outcomes, failure isolation, and RPO/RTO. During partitions, identify which operations reject, wait or continue and which invariants they preserve. Do not reduce CAP to an unconditional product label.

## State, concurrency and delivery

- Replicas add lag, failover and split-brain questions. Sharding adds routing, hot keys, rebalancing and cross-shard work. Prefer database-native capabilities until capacity evidence justifies more.
- Never infer global ordering from wall clocks. Use explicit ordering scopes and stable identifiers. Distributed leases require expiry, renewal/crash behavior and fencing when stale owners could still write.
- A timeout leaves an operation's outcome unknown. Reconcile with authoritative state before repeating an external effect.
- Scope idempotency to actor/tenant, operation and meaningful request identity. Reject mismatched payload reuse. Persist outcome and handle concurrent duplicates; define pending states, retention and replay windows.
- Separate transport delivery from the business effect. At-least-once delivery generally requires idempotent consumers, durable deduplication and a replay path. Claims of exactly-once behavior need a named boundary and evidence.
- Events describe facts; commands request work. Define schema/version, producer/consumer ownership, ordering scope, dedupe identity, replay/backfill, retention and poison-message handling.
- A transactional outbox closes the local write/publication gap; a publisher crash may still redeliver. Sagas coordinate compensations whose effects and failure recovery must be modeled; they do not restore global atomicity.

Do not invent a consensus algorithm or distributed transaction coordinator for ordinary application work.

## Bound overload and recovery

Propagate deadlines and cancellation. Bound queues, worker concurrency, connections and per-tenant resource use. Set admission control, load shedding and bulkheads where needed. Retry only eligible failures within an attempt and total-time budget, using backoff and jitter; pick one appropriate retry owner to avoid multiplying attempts across layers. Circuit breakers do not replace timeouts or capacity controls.

For jobs define acknowledgment/visibility semantics, retry limits, DLQ ownership, safe replay, cancellation, lag monitoring and recovery from worker death. Keep latency-sensitive and bulk workloads from exhausting the same pool when isolation matters.

## Cache and building-block contracts

Before adding a cache define source of truth, complete key identity including tenant/access context, TTL, invalidation, acceptable staleness, warm-up, eviction/memory cap, stampede protection, failure fallback and metrics. Test permissions changing while entries remain cached. A shared CDN must not serve private content to another user.

| Component | Introduce when | Resolve before adopting |
|---|---|---|
| Load balancer | Multiple serving instances | Readiness, connection draining, affinity and skew |
| Queue | Bursts, decoupled work, durable retry | Duplicate effects, lag, bounded backlog and replay |
| Object store | Durable blobs and artifacts | Access control, lifecycle, upload/download safety |
| Search index | Real full-text/relevance needs | Source synchronization, ACLs, versioning, rebuild |
| Workflow engine | Durable long-running coordination | State migration, idempotency, engine operations |
| Service mesh | Repeated service policy at sufficient scale | Control-plane ownership and failure cost |
| Kubernetes | Orchestration needs exceed simpler hosting | Cluster operations, security, recovery and cost |

## Common scenarios and evolution triggers

- **Uncertain-scale SaaS:** modular backend, transactional store, object storage, managed hosting; add workers where latency or durability requires them. Extract services when a measured bottleneck or ownership boundary pays for the cost.
- **Read-heavy content:** query/index work, then eligible CDN/cache; replicas when primary read load is the actual constraint. Decide freshness and privacy first.
- **Payments/orders:** explicit state machine, durable intent and provider IDs, verified webhooks, scoped idempotency and reconciliation. Timeout means pending/unknown, not automatic failure. Use a ledger when tracking balances.
- **Notifications:** bounded delivery workers, quotas, preferences/consent, dedupe, delivery states and DLQ replay. Provider acceptance does not establish delivery.
- **B2B multitenancy:** identity-derived scope through queries, search, caches, jobs, exports and administration; isolation tests and per-tenant quotas.
- **Regional availability:** explicit failure domains and data ownership, multi-zone durability as appropriate, tested restore/failover. Active-active writes require an actual conflict/consistency design.
- **Enterprise integration:** vendor adapter, stable contract, credential isolation, quotas, signature checks, compatibility and reconciliation.
- **Company-data copilot:** enforce corpus ACLs before retrieval; bound tools, evaluate groundedness and preserve authorization through actions.

Revisit designs on observed triggers: sustained saturation, SLO burn, team ownership changes, budget deviation, new legal constraints or incident learning. Compare total operating cost, not only deployment convenience.

## Foundations

[C4](https://c4model.com/), [AWS Well-Architected](https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html), [Azure Well-Architected](https://learn.microsoft.com/en-us/azure/well-architected/), [Google Cloud Architecture Framework](https://cloud.google.com/architecture/framework). Adapted from master §§10–11, 26 and 37. Verify platform-specific guarantees against the deployed version.
