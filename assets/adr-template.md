# ADR-[number]: [decision]

Status: [proposed / accepted / superseded by ADR-number]
Date: [YYYY-MM-DD, timezone if material]
Owner / decision authority: [name or role]
Scope / related issue: [affected capability and links]

> Copy and adapt this template for a consequential decision. Replace bracketed fields with facts or labeled unknowns; remove inapplicable sections. A proposed ADR does not establish approval or implementation.

## Context and constraints

[Problem and desired user/business outcome. Current implementation and why a decision is needed now.]

| Driver | Known / estimated / unknown | Constraint or evidence |
|---|---|---|
| Correctness/security invariants | [state] | [rules and trust boundaries] |
| Workload and service levels | [state] | [units, observation window, environment] |
| Team, budget and deadline | [state] | [limits and ownership] |
| Compatibility and recovery | [state] | [affected consumers/data and irreversible points] |

Non-goals: [deliberate exclusions]

## Options and trade-offs

| Option | Correctness/security | Complexity/operations | Cost/time | Compatibility/reversibility |
|---|---|---|---|---|
| [simplest viable baseline, including no change if viable] | [evidence or uncertainty] | [cost] | [assumptions] | [transition] |
| [credible alternative] | [evidence or uncertainty] | [cost] | [assumptions] | [transition] |

## Decision and rationale

[Chosen option and decisive drivers. Why the extra complexity, if any, pays for itself. Which evidence supports the choice and what remains estimated.]

## Consequences and risk ownership

Benefits: [observable improvements]
Costs / limitations: [ongoing operating, coordination or lock-in costs]
Residual risks / owners: [impact, compensating control, review trigger]
Authorized exceptions, if any: [rule, authority, scope, reason, control, expiry, evidence]

## Transition and recovery

[Incremental rollout, old/new coexistence, data migration/reconciliation and retirement. Abort signals, rollback prerequisites/limits and forward repair after irreversible changes. Execution authority is separate from this proposal.]

## Validation and acceptance

| Claim / acceptance criterion | Method or exact command | Evidence / state | Limitation / owner |
|---|---|---|---|
| [observable behavior] | [test, rehearsal, measurement or review] | [executed result or NOT RUN] | [remaining gap] |

## Revisit when

[Observable threshold, incident, workload, cost, team or policy change that invalidates assumptions. Name owner/review date where useful. Link the superseding decision rather than silently rewriting history.]
