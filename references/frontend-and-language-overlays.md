# Frontend and language overlays

Use only the overlay for the actual runtime/framework. Contents: browser state; accessibility/localization; TypeScript/Node; Java; Python; Go; Rust; SQL; React/Next; mobile.

Inspect package manifests, lockfiles, configuration, deployment and existing idioms first. Examples and defaults are not version guarantees. Verify current authoritative documentation for version-dependent APIs; do not migrate the stack as an incidental part of another task.

## UI states, ownership and access

Define initial, loading, empty, success, partial success, transient/permanent failure, stale data, permission denied, offline, session expiry and concurrent-edit states when relevant. Give users useful retry/recovery paths. Optimistic changes need reconciliation and reversal; stale responses must not overwrite newer state after navigation or repeated requests.

Separate presentation, coordination, domain rules and IO where it makes state ownership clearer. Prefer local state for local concerns, deliberate shared state for true shared ownership and a server-state cache when its coordination benefits justify it. Avoid overcomponentization and unnecessary global stores.

Use semantic HTML, accessible names, keyboard operation, visible focus, correct focus movement, announced status/error changes, adequate contrast and reduced motion. Declare the applicable WCAG target for the product/jurisdiction. Automated checks are useful but do not replace manual keyboard and assistive-technology checks for critical flows.

Preserve localization needs for dates, pluralization, numbers, currencies, content expansion and RTL when in scope. Store instants independently of display locale; scheduled local time may need an explicit timezone and daylight-saving policy. Avoid hardcoded parsing of locale-formatted text.

## TypeScript / Node.js / NestJS

- Prefer strict types and `unknown` for untrusted values; parse external JSON, HTTP, messages, webhooks and configuration with runtime schemas. Type assertions and DTO annotations do not make input trustworthy.
- Bound concurrent promises/tasks and worker resources. Avoid expensive synchronous work on the event loop; CPU-heavy work may require bounded workers. Propagate cancellation, handle rejections and close resources on shutdown.
- Keep error mapping consistent, diagnostic logging correlated and safe, controllers thin and policy explicit. In NestJS, use pipes/guards/interceptors/filters for their actual roles without hiding business invariants in a giant injectable service.
- Keep ORM transaction semantics explicit and separate persistence shapes from public contracts.
- Inspect ESM/CJS and module resolution configuration; run built output where source-only execution can mask deployment failures. Use the project's supported runtime and locked package manager.

## Java / Spring Boot

Use coherent capability packages, validated DTOs, explicit transaction boundaries and suitable immutable value types. Check transaction proxy boundaries and actual database behavior where relevant. Bound executor and connection pools. Measure ORM fetch plans; hidden lazy queries/open-session-in-view can disguise N+1 costs. Verify the effective Spring Security policy and failure semantics, not only annotations. Integrate against the real database for isolation-sensitive behavior.

## Python / Django / FastAPI

Use type hints plus runtime validation at external boundaries as appropriate. Inspect async/sync transitions and prevent blocking calls from exhausting event-loop or worker capacity. Scope ORM querysets by authorization/tenant and transactions by invariant. Bound background work and align worker deployment, request deadlines and shutdown behavior. Lock/pin dependencies reproducibly according to the project tooling.

## Go

Propagate context deadlines/cancellation; bound goroutines/channels and define ownership/closure. Close resources, wrap errors while preserving causes and make cleanup paths visible. Prefer small consumer-defined interfaces and explicit composition. Run the race detector for concurrency-sensitive changes when available; a clean race run does not prove every interleaving safe.

## Rust

Use ownership, explicit result types and domain types to protect invariants. Keep `unsafe` minimal, justified and documented with its safety contract. Review async cancellation, blocking work, resource lifetimes and FFI/untrusted boundaries. Benchmark optimized builds under representative conditions, not debug-only timings.

## SQL and data access

Use typed parameters, constraints and migration-controlled schemas. Allowlist identifiers that cannot be parameters. Verify execution plans on meaningful cardinality, isolation/locking for the invariant and DDL rewrite/lock implications. Do not replace real database tests with ORM mocks for race-sensitive work.

## React / Next.js and browser security/performance

Make client/server trust boundaries explicit. Server-rendered routes and server actions still need runtime input validation and server-side authorization. Do not bundle secrets or use hidden UI as the only permission control. Guard user HTML, uploads and unsafe DOM operations; choose cookie/CSP/cache behavior from the security model, including authenticated responses.

Handle aborted/stale data requests, hydration mismatches and render/error states. Measure real-user Core Web Vitals where available, inspect image formats/dimensions, bundles, data-fetch waterfalls, caching and hydration cost. Adopt SSR/edge/preload for a concrete improvement rather than as a blanket default.

## Mobile / cross-platform

Plan for offline synchronization, conflicts, app lifecycle, network/battery variability and background limits. Store credentials in supported secure OS storage; shipped binaries cannot keep privileged secrets. Account for app-store release lag and older clients in API evolution. Verify accessibility on the target platform and safe cancellation/retry when connectivity changes.

## Foundations

[WCAG](https://www.w3.org/WAI/standards-guidelines/wcag/) is a starting point for the declared accessibility target. Use the official docs for the installed language/framework when implementing details. Adapted from master §§21–22; these overlays refine the constitution rather than mandate every practice for every project.
