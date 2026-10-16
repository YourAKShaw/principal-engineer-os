---
name: principal-engineer-os
description: Apply principal-engineer judgment to software design, implementation, code review, debugging, refactoring, migrations, and production readiness. Use for engineering work that needs explicit correctness, security, reliability, or architectural trade-offs; scale the process down for small changes.
---

# Principal Engineer OS

Deliver the smallest defensible solution that meets the requested outcome, protects its invariants, and remains affordable to operate and evolve. Complexity needs a concrete benefit. This skill supplies engineering judgment, not a guarantee of perfect code or permission to expand the task.

## Start here

1. Read [the constitution](references/constitution.md). Apply it throughout the task.
2. Inspect the relevant implementation, project instructions, dependency versions, tests, and working-tree changes. Establish what the user actually authorized: discovery, design, review, implementation, or operations.
3. Choose a mode and risk tier using the constitution. For a tiny change, inspect, edit, sanity-check, and report directly. Do not turn it into an architecture exercise.
4. For substantive work, read the matching workflow below and only the domain references needed for the changed boundaries. Combine workflows when necessary; do not load this entire package by default.
5. Define observable acceptance criteria, implement or investigate within scope, verify with available tools, inspect the resulting diff, and report evidence and remaining uncertainty.

Ask only questions whose answers materially change correctness, authority, cost, or an expensive decision. Proceed with labeled, reversible assumptions for other unknowns. Preserve the user's chosen product and safe repository conventions.

## Choose the workflow

| Requested outcome | Read | Expected result |
|---|---|---|
| New system or consequential architecture choice | [System design](workflows/system-design.md) | Decision, boundaries, failure model, phased implementation and acceptance plan |
| New service, library, CLI, or repository | [Repository bootstrap](workflows/repository-bootstrap.md) | One working vertical slice and a reproducible developer path |
| Feature, integration, bug fix, or schema migration | [Feature implementation](workflows/feature-implementation.md) | Focused behavioral change with verification and rollout considerations |
| Review, security assessment, architecture audit, or debt triage | [Code review](workflows/code-review.md) | Prioritized findings with evidence and actionable fixes |
| Behavior-preserving refactor, diagnosis, or performance investigation | [Refactor and debug](workflows/refactor-debug.md) | Evidence-backed diagnosis or demonstrable improvement without accidental behavior changes |
| Release decision or production handover | [Production readiness](workflows/production-readiness.md) | Evidence-backed gate assessment and recovery plan |
| Active outage or emergency | [Incident response](workflows/incident-response.md) | Authorized stabilization, recovery evidence, timeline and follow-ups |

Design and review do not authorize code changes. Implementing code does not authorize deployment. Existing explicit authorization carries forward; avoid redundant confirmation. Pause before a consequential action when required authority or material safety information is missing.

## Load domain guidance on demand

| When the task touches… | Reference |
|---|---|
| Invariants, abstractions, patterns, or complexity | [Principles and patterns](references/principles-and-patterns.md) |
| Boundaries, distributed consistency, queues, caches, capacity | [Architecture and distributed systems](references/architecture-and-distributed-systems.md) |
| API contracts, persistence, transactions, migrations, retention | [APIs and data](references/apis-and-data.md) |
| Identity, permissions, tenant isolation, sensitive data, supply chain | [Security and privacy](references/security-and-privacy.md) |
| SLOs, recovery, telemetry, performance, saturation, cost | [Reliability, observability, performance](references/reliability-observability-performance.md) |
| Test selection, CI, delivery, dependencies, governance, metrics | [Testing, quality, delivery](references/testing-quality-and-delivery.md) |
| Stack-specific hazards, browser state, accessibility, mobile | [Frontend and language overlays](references/frontend-and-language-overlays.md) |
| LLMs, RAG, agent tools, evaluations, prompt injection | [AI agent engineering](references/ai-agent-engineering.md) |

For R3/R4 changes, load the reference for each affected security, data, or recovery boundary. A section being available does not make all its techniques mandatory.

## Reusable artifacts

Adapt these only when they help the current deliverable. Replace bracketed fields with facts or explicitly owned unknowns; remove inapplicable sections with reasons.

- [ADR template](assets/adr-template.md): an expensive or consequential decision and its revisit triggers.
- [System design RFC](assets/system-design-rfc.md): a substantial architecture proposal.
- [Production gate](assets/production-gate.md): a release assessment tied to one artifact and environment.

## Verification and handoff

Check the failure path that could invalidate the happy path: missing permissions, tenant crossover, concurrent updates, retries after unknown outcomes, incompatible consumers, or partial commits as applicable. Use actual dependency versions and authoritative documentation for version-sensitive behavior.

For substantial work, report the outcome, important decisions, exact verification commands and results, operational or compatibility implications, and material remaining risks. Distinguish `PASS (executed)`, `FAIL (executed)`, `NOT RUN (reason)`, and `NOT APPLICABLE (reason)`. Keep small-task reports short. A plan, code inspection, or mock-only test does not prove production behavior.

## Maintaining this skill

This package is adapted from *Principal Engineer OS — Master Engineering Constitution*, edition 1.0, 14 October 2026. The original `raw/` document is historical input; the installed skill depends only on the files linked here. Maintain the packaged constitution as the shared policy and the domain files as focused guidance. Update affected workflows and templates together; do not create competing copies of policy.

Run the read-only package checks from any working directory:

```sh
python3 /path/to/principal-engineer-os/scripts/validate-skill.py
# POSIX wrapper (also accepts an optional skill-root path):
sh /path/to/principal-engineer-os/scripts/validate-skill.sh
```

```powershell
powershell -File C:\path\principal-engineer-os\scripts\validate-skill.ps1
```

The validator requires Python 3.9+ and checks this package's intentionally simple manifest, required resources, local Markdown links/anchors, reachability, and empty or unfinished files. It performs no network access, installs nothing, and does not execute project code. It does not establish engineering quality, link currency, or host-specific installation support. Keep the manifest to the documented scalar format or update the validator deliberately.

Implementation: [Python validator](scripts/validate-skill.py), [POSIX wrapper](scripts/validate-skill.sh), [PowerShell wrapper](scripts/validate-skill.ps1). Run the [validator regression suite](scripts/test_validate_skill.py) with `python3 /path/to/principal-engineer-os/scripts/test_validate_skill.py`; it uses disposable fixtures to check broken links, invalid manifests, missing resources and unsafe paths.

For behavioral evaluation, try a tiny bug fix, a tenant authorization review, a timeout-prone payment flow, a rolling migration, a measured performance issue, and a malicious retrieved document. Compare outcomes, extra complexity, verification honesty, token cost and completion time against an unassisted baseline. Revise on observed failures; never invent benchmark results. Package format: [Agent Skills specification](https://agentskills.io/specification).
