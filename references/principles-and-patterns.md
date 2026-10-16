# Principles, patterns and complexity

Use when choosing boundaries, abstractions or refactors. Contents: invariants; design principles; pattern selection; anti-patterns; decision evidence.

## Start with invariants and reasons for change

Identify the state owner and the rule that must remain true. Keep policy close to the state it protects; put transport, persistence and external integrations at deliberate boundaries. Prefer deterministic business rules with an imperative IO shell where it clarifies testing. Construct trusted internal values by parsing once at boundaries. Use types, constraints and explicit state machines to prevent invalid states, while recognizing that static types do not validate external data.

High cohesion means behavior changes for a coherent reason. Low coupling means callers depend on intentional contracts rather than mutable internals. An abstraction earns its place when it serves real variation or enforces a significant boundary; it need not have two callers to justify a security boundary.

## Apply principles to decisions

| Principle | Useful interpretation | Failure to avoid |
|---|---|---|
| SRP | Keep behavior that changes together together | Tiny forwarding classes scattered across layers |
| OCP | Add extension points for recurring variation | Plugin framework for one conditional |
| LSP | Subtypes preserve behavior, invariants and errors | Inheritance that surprises existing callers |
| ISP | Interfaces follow consumer capabilities | One enormous service facade |
| DIP | Policy depends on stable capabilities at real boundaries | Interface per class or a service locator |
| KISS / YAGNI | Minimize concepts and defer hypothetical features | Deleting necessary controls in the name of simplicity |
| DRY | Centralize shared knowledge and invariants | Coupling unrelated code because its syntax resembles other code |
| Composition | Assemble explicit collaborators | Deep inheritance or invisible wrapper stacks |
| Information hiding | Expose capabilities, protect mutable state | Leaking ORM entities or internal collections |
| Least astonishment | Make side effects, time, retries and errors explicit | Hidden network IO behind ordinary property access |
| Law of Demeter / tell, don't ask | Offer behavior rather than navigating internal graphs | Mechanical prohibition of all data access |

Make public interfaces narrow and domain-oriented. Avoid boolean-argument combinations that encode hidden modes; choose named options or explicit operations. Do not hide business policy in generic helpers. Fail closed for permission checks and choose a safe, explicit degraded behavior for operational failures.

## Patterns are conditional tools

For any consequential pattern name the problem, required variation, cost and removal/evolution trigger.

| Need | Candidate | Important cost or caveat |
|---|---|---|
| Interchangeable policies | Strategy | A simple conditional may be clearer |
| Context-dependent object creation | Factory; builder for complex validated construction | Indirection can hide easy constructors |
| Vendor interface differs from domain capability | Adapter / anti-corruption layer | Do not wrap everything without isolating actual semantics |
| Coherent subsystem entry point | Facade | Avoid a mixed-concern god service |
| Composable cross-cutting behavior | Decorator | Preserve visible ordering and failure semantics |
| Recursive structure | Composite | Do not invent a hierarchy for flat data |
| Independent reactions to a fact | Observer / pub-sub | Ordering, hidden effects, delivery and replay need contracts |
| Durable, retryable or auditable action | Command | A command bus is unnecessary for simple CRUD |
| Meaningful lifecycle-dependent rules | State machine / State | Explicit transitions beat combinations of flags |
| Stable algorithm with subtype variation | Template Method | Prefer composition when inheritance weakens contracts |
| Domain-oriented persistence boundary | Repository | Generic CRUD can obscure important query/transaction behavior |
| Persistence transaction coordination | Unit of Work | Do not duplicate the ORM's semantics |
| Reused composable domain predicates | Specification | Avoid an opaque homegrown query language |
| Collaborator substitution and lifetime | Dependency injection | Explicit construction often suffices |
| Dense peer coordination | Mediator | Central coordination can become a god object |
| Controlled access or remoting | Proxy | Expose consequential latency and side effects |
| Dependency failure containment | Circuit breaker / bulkhead | Still require timeouts and resource sizing |
| Transient, safe retry | Backoff with jitter | Bound attempts, total deadline and amplification |
| Atomic local write and eventual publication | Transactional outbox | Consumers still need deduplication |
| Multi-service process | Saga / durable workflow | Compensation is not transactional rollback |
| Materially different read/write requirements | CQRS | Separate models add synchronization and operating cost |
| Business-critical history and replay | Event sourcing | Schema evolution, replay safety and projection operations are substantial |
| Proven hot reads with tolerable staleness | Cache-aside | Invalidation, stampedes and access-control context |
| Incremental legacy replacement | Strangler | Define routing, state ownership and retirement criteria |

## Review complexity across the whole system

Count infrastructure, deployed units, protocols, dependency edges, coordination, consistency models and on-call burden as well as code. Cleaner local code can make the system harder to operate. Conway's law suggests aligning boundaries with actual team communication and ownership; Gall's law favors evolving working slices over unproven big-bang systems. Amdahl's law reminds performance work to address meaningful end-to-end costs.

Investigate god objects, scattered invariants, premature services, a shared schema with independent release claims, cycles, global mutable state, fragile inheritance, generic repositories hiding queries, unbounded queues, N+1 calls, long synchronous dependency chains, swallowed exceptions, side-effectful imports, configuration sprawl and flags without owners or expiry. These are investigation signals, not automatic findings.

For a refactor, state the observed maintenance problem, a behavior baseline, the intended reduction in complexity and how parity will be checked. Do not replace a safe repository idiom just to enforce a preferred pattern.

## Foundations

Use these for deeper context, verifying relevant details when needed: [Fowler's enterprise patterns](https://martinfowler.com/eaaCatalog/), [DDD Reference](https://domainlanguage.com/ddd/reference/), and [Strangler Fig](https://martinfowler.com/bliki/StranglerFigApplication/). This reference adapts master constitution §§6, 8–9, 24 and 36; it is guidance rather than a checklist to apply wholesale.
