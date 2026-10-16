# APIs, persistence and data evolution

Use for contracts, external integrations, database changes and data lifecycle. Contents: interface semantics; concurrency; integrations; storage; migrations; recovery.

## Specify an observable contract

Before writing handlers, define actors and permission scopes, request/response schemas, state transitions, errors, idempotency, pagination, filtering, rate limits and compatibility. Keep transport DTOs separate from persistence objects. Parse runtime inputs and enforce authorization at the use-case/data boundary; type declarations alone do neither.

For HTTP, preserve safe GET semantics. Define PUT replacement, PATCH partial-update rules and DELETE idempotent intent deliberately. Creation/actions with POST may need an idempotency contract. Use consistent status semantics: malformed input, missing/invalid authentication, forbidden access, absent/hidden resources, conflicts, semantic validation, quotas and server errors. Hide resource existence where the threat model requires it. A successful request must not conceal a failed effect.

Errors need stable machine codes, safe messages, correlation and useful field details; keep stack traces, SQL and secrets in protected diagnostics. RFC 9457 Problem Details is an option when it fits the API. Do not adopt a new error envelope solely for one endpoint in an otherwise consistent safe project.

## Lists, concurrent edits and protocol choices

Bound page sizes, filter complexity and expensive sorts. For changing or large ordered data prefer cursor pagination with a deterministic tie-breaker; offsets can be adequate for small administrative lists. Cursors must not bypass tenant scope. Specify empty, exhausted and invalid-cursor behavior.

Use version checks, ETags/If-Match, suitable transaction isolation or locks for competing updates. Report conflicts instead of silently losing changes. Test two clients editing the same version, including deletion and stale data.

| Interface | Fits when | Essential controls |
|---|---|---|
| HTTP/REST | Resource/action contracts and broad clients | Cache semantics, status/error consistency, version support |
| GraphQL | Composable client projections justify it | Field auth, depth/complexity limits, batching to prevent N+1 |
| gRPC | Typed internal contracts/streaming add value | Deadlines, retry safety, protobuf compatibility |
| WebSockets/SSE | Real-time delivery is actually needed | Auth refresh, connection caps, ordering/replay, reconnect, backpressure |

Prefer simpler polling if it meets the user's latency and load needs.

## External effects and contract evolution

Isolate vendor payloads behind a meaningful adapter. Set connect/read/overall time budgets, eligible retry rules and quota handling. Verify webhook signatures on the required bytes, enforce freshness/replay policy, and persist provider identifiers alongside internal identities. Test out-of-order and duplicate callbacks. An external request inside a database transaction does not become atomic with that transaction.

For additive changes, choose defaults that preserve existing meanings. Do not silently repurpose fields. Define deprecation windows, support/sunset policy, consumer contract checks and staged compatibility for old binaries, jobs and clients. A tolerant consumer must not tolerate unsafe privilege or state changes.

## Choose storage from workload and invariants

A relational database is a useful transactional default. Choose document, key-value, graph, wide-column, time-series, search or analytical storage for a specific access/scale/consistency advantage, with operational cost acknowledged. Begin from query shapes, relationships, atomic rules, volume, durability and team capability.

- Model keys, uniqueness, foreign keys, required fields, ownership and lifecycle explicitly. Enforce critical race-sensitive invariants with database constraints as well as application rules.
- Use exact monetary representations (decimal or integer minor units with currency rules), sufficient integer widths and explicit instants/timezones. Avoid float equality for money and reinterpretation of local timestamps during migrations.
- Deliberately choose restrict/cascade behavior. Soft deletion changes uniqueness, filters, indexes, retention and legal deletion; it is not a free substitute for lifecycle design.
- Normalize transactional data to avoid inconsistent updates; denormalize when measured access patterns justify maintaining copies.
- Match indexes to predicates, ordering, selectivity and volume. Inspect plans on representative data; prevent N+1, unbounded scans and accidental casts. Every index adds write/storage cost.

## Transactions and idempotency

Identify the invariant before choosing isolation. Understand the actual database's lost-update, write-skew, phantom and deadlock behavior. Pick constraints, optimistic versions, row locks or serializable transactions as required. Retry serialization/deadlock failures only when the whole operation can safely repeat within a bound.

For balances, a transfer needs atomic debits/credits, correct concurrency and a durable audit trail; a double-entry ledger is appropriate when financial accountability is required. A unit test mocking SQL cannot establish isolation or locking behavior.

For retryable requests, persist scoped request identity and outcome durably, coordinate concurrent duplicates, reject payload/key conflicts and reconcile unknown external outcomes. Retention/dedupe windows must match the real retry horizon.

## Safe migrations: expand–migrate–contract

Apply this lifecycle to schema evolution, data backfills and stateful refactors:

1. **Design:** inventory old/new schemas and every reader/writer, including jobs and older clients. Estimate affected volume, lock/disk/replica impact, ownership and abort triggers.
2. **Expand:** add compatible structures. Verify database-specific online/concurrent DDL behavior for the deployed version; an additive column can still lock or rewrite a large table.
3. **Dual compatibility/shadow:** deploy code that works during mixed-version rollout. If dual writing is necessary, choose authoritative state and reconcile divergence; do not assume two writes are atomic.
4. **Backfill:** use stable cursors, bounded idempotent batches, checkpoints, safe retries, rate limits and progress/error metrics. Account for new writes, updates and replica lag. Avoid one unbounded transaction.
5. **Verify and cut over:** compare invariants, counts and meaningful checksums/samples, repair discrepancies, then change authority with staged observation.
6. **Monitor, contract, retire:** remove old paths only after all consumers and cached representations migrate and the recovery window closes.

Rehearse high-risk work at representative volume and concurrent load. Record rollback limits and a forward-repair strategy after irreversible transformation. A down migration that drops new data is not recovery.

Watch normalization/uniqueness changes, timezone conversion, narrowed enums, new defaults, orphaned rows, ORM auto-DDL, index locks, stale cache objects and old event writers. A migration is complete only after reconciliation and retirement, not merely after the script exits.

## Lifecycle, backups and analytical work

Classify data and owners; define minimization, access, encryption, retention/deletion, export and legal holds. Explain realistic deletion propagation into caches, replicas and backups. Do not copy production personal data into lower environments without the required authorization and controls.

Define RPO/RTO, backup freshness, point-in-time recovery where needed, isolated recovery copies, access permissions and restore dependencies. Restore into a clean environment and measure the result. Backup job success does not prove recoverability.

Keep heavy analytics from exhausting OLTP capacity. Replicas, CDC or a warehouse can help when justified; account for lag, schema drift, attribution and sensitive-data propagation.

## Foundations

[RFC 9457](https://www.rfc-editor.org/rfc/rfc9457), [OpenAPI](https://spec.openapis.org/oas/latest.html), [Protocol Buffers](https://protobuf.dev/programming-guides/), [PostgreSQL docs](https://www.postgresql.org/docs/). Adapted from master §§7, 12–13 and 32. These are entry points; verify behavior against the actual technology and version.
