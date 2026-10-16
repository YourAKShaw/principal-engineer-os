# Testing, quality and delivery

Use to choose evidence, CI, dependency controls, delivery practices or engineering metrics. Contents: test selection; test design; reproducibility; release safety; maintainability and governance.

## Pick evidence for the risk

Tests establish behavior under their conditions; counts and coverage percentages are not correctness. Use the cheapest layer that can reveal the relevant failure without mocking it away.

| Risk or question | Useful evidence |
|---|---|
| Deterministic rule, parser, accounting invariant | Unit/property-based tests, boundary and overflow cases |
| Module state transitions | Component tests with meaningful collaborators |
| Database constraints, isolation, queries | Real datastore integration and concurrency tests |
| API/event compatibility | Contract tests for deployed producer/consumer versions |
| Critical user journey | A small set of stable, representative E2E tests |
| Malformed/adversarial inputs | Fuzzing, schema and abuse tests |
| Duplicate effects or competing writes | Controlled interleavings, durable-state and replay assertions |
| Data evolution | Mixed-version, backfill, preservation and recovery rehearsal |
| Capacity/leaks | Representative load/soak measurement |
| Dependency failure/recovery | Timeout, partial success, outage, replay and restoration tests |
| Browser access | Automated checks plus manual keyboard/assistive-tech verification |

A library, data-heavy service and UI need different portfolios. The test pyramid is a cost/confidence heuristic, not a mandated ratio. For reversible text-only changes, a contextual sanity check may be sufficient.

## Make tests detect real failures

Choose boundary values, equivalence classes, decision tables, state transitions and negative paths. Cover relevant null/empty states, ordering, timezones, overflow, cancellation, permissions and conflicts. Use controlled clocks, seeded randomness, isolated data and synthetic credentials. Assert observable semantics rather than incidental implementation details or broad snapshots.

Use fakes for controlled behavior, stubs for known results, spies for required effects, and mocks when interaction itself is the contract. Keep some actual integration evidence for the risky boundary: mocking a database cannot prove its transaction semantics, and mocking an HTTP client cannot prove a provider accepts the request.

For a bug, reproduce before fixing where feasible and show the regression test distinguishes old/new behavior. For a refactor, characterize behavior before moving it. If a failure is pre-existing, establish that with evidence and report it; do not weaken the assertion or security control to make the build green.

Run focused checks, then impacted broader checks. Repeat only when new changes, failures or unresolved concerns justify it. Record exact commands, environment and `PASS`, `FAIL`, `NOT RUN` or `NOT APPLICABLE` with reasons. Distinguish code inspection, simulation and production observation.

## Reproducible development and CI

An unfamiliar engineer should be able to install, configure safely, build, test and run the project from accurate documentation. Use supported runtimes, committed lockfiles as appropriate, configuration validation and example values without secrets. Separate development/build/production dependencies. Evaluate maintenance, licensing, transitive risk and upgrade cost before adding a package; built-ins may suffice.

A proportionate CI pipeline checks the immutable source, installs locked dependencies, runs formatting/lint/types and meaningful tests, validates contracts/schemas, performs applicable dependency/secret/security checks and builds an immutable artifact. Record source/version/build provenance when needed. Restrict runner and publication credentials and protect trusted branches/environments. Never expose secrets to untrusted pull-request execution.

Cache dependencies safely; deterministic installation must not silently refresh the dependency graph. Validate generated output and built runtime behavior where compilation/transpilation alone can miss a deployment problem.

## Delivery and operating environment

- Externalize config/secrets and validate required settings at startup. Keep durable state in appropriate stores and deployment artifacts immutable. Apply twelve-factor ideas pragmatically.
- Containers should use maintained minimal bases, controlled versions, non-root execution, signal-aware shutdown, relevant health/resource settings and no baked credentials. Isolation is not an absolute security boundary.
- Review IaC plans, constrain IAM, pin providers/modules, protect state, separate environments and reconcile emergency manual changes. Avoid destructive wildcard scope.
- Choose environment count from risk and team capacity. Keep production personal data and real charge/send credentials out of test flows unless explicitly authorized and controlled.
- Separate deployment from user release. Use flags, canaries, dark launches or blue/green where useful; assign flag owners and expiry.
- Before rollout know artifact/commit, environment/config, migration order, monitoring owner/window, health/smoke checks, abort triggers and rollback/roll-forward steps. Old binaries, jobs and long-lived/mobile clients must remain compatible during transition.

## Repository health, governance and debt

Keep module APIs, allowed imports, ownership and state boundaries explicit. Avoid cycles and a shared catch-all utilities package. For monorepos define build/release graph and selective checks; for multiple repositories define contract publication and rollout order.

Add documentation for actual needs: setup and commands, glossary and system map, API contracts, decisions and critical runbooks. CONTRIBUTING, SECURITY, CODEOWNERS and architecture documentation help when used; do not manufacture a file forest for a tiny utility. Keep examples current and executable.

Use lightweight governance: paved paths, owned standards, reviewed exceptions and objective checks. Fitness functions may enforce import direction, schema/API compatibility, migration constraints, resource budgets or security controls. Prose policy alone is not enforcement. Match service count and on-call responsibilities to real team capacity.

Track conscious debt with impact, ongoing cost, owner and revisit trigger. Prioritize observed harm to correctness, security, reliability or delivery over stylistic preferences. For compliance, map applicable controls to evidence with qualified input; do not claim certification from a checklist.

## Metrics that inform decisions

Use trends and consistent cohort/window definitions. Delivery lead time/frequency and change size describe flow; change-failure rate and recovery time describe safety. Combine SLO burn/user impact with tail latency, saturation and queue lag. Track exposure age for security, escaped defects and flakiness for tests, review friction/coupling for maintainability, and cost per useful transaction for operations. AI eval success, grounding failures and tool success need representative task context.

Define each numerator, denominator and population; arbitrary universal targets encourage gaming. Code coverage, scanner counts, deployment frequency and benchmark leaderboards each miss important dimensions of quality.

## Foundations

[GitHub Actions security](https://docs.github.com/en/actions/security-guides/security-hardening-for-github-actions), [Twelve-Factor App](https://12factor.net/), [DORA](https://dora.dev/). Adapted from master §§18–20, 24–25 and 35–36. Match checks and platform controls to actual project support.
