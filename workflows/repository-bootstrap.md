# Bootstrap a repository

Use for a new service, library, SDK, CLI or application. An existing repository is not a blank canvas: inspect and preserve its working-tree changes and policies first.

## Choose the smallest useful baseline

Establish artifact type, target users/runtime/deployment, primary capability, persistence/integration needs, team skills and expected risk. Respect stated stack constraints. If the stack is unspecified, choose a supported familiar baseline and state the assumption; verify current version/support details before pinning.

Use the relevant language overlay. Add domain references for actual persistence, authorization, external effects or AI features. Do not add a database, queue, container cluster or monorepo merely to make the scaffold appear complete.

Choose package/module boundaries from business capabilities and actual build/release needs. For a small CLI, one package may be enough. For a monorepo, define package ownership, allowed dependencies and build/test/release graph.

## Implement a real vertical slice

Build the first requested behavior through its real entry point, validated input, domain rule, state/persistence if needed, output/error path and verification. For a service this may include authorization, database transaction and handler; for a library it may be a public API and contract tests. Do not invent an unrelated sample domain or ship fake TODO methods as functionality.

Use the working slice to establish conventions for:

- Runtime/config parsing and safe example values; required settings fail clearly.
- Coherent state ownership, errors and appropriate static types.
- Structured diagnostics and trace/request context when network-facing.
- Focused tests, plus a realistic integration path for risky boundaries.
- Resource lifecycle, readiness and graceful shutdown for services.

Then add reproducible runtime/package-manager versions, lockfiles and useful formatting/lint/type/test/build scripts. Keep dependencies intentional; inspect installation scripts and respect network/workspace permissions.

## Make the developer path reproducible

Write accurate setup/run/check commands, configuration descriptions, architecture rationale and limitations. Add security reporting, contribution or ownership documents when there is a concrete need. Use minimal containers/dev environments when they improve setup, not automatically.

Configure CI to execute the project's actual checks with locked dependencies and least privilege. Deployment definitions belong only when requested or needed for the agreed artifact; provisioning paid resources and deploying require adequate authorization.

Verify the install/build/check/run path in a clean isolated environment when practical. Do not delete existing work or run real charge/send workflows to simulate a clean setup. If credentials/tooling are missing, document the exact limitation and what was verified instead.

## Completion evidence

Check that an unfamiliar engineer can follow the documentation; the first real capability works under tested conditions; inputs/config and relevant access boundaries are enforced; errors and resource cleanup are visible; CI matches local commands; migrations run if present; no secrets/fake implementations or unnecessary infrastructure were introduced.

Report files/behavior delivered, stack assumptions, executed commands/results, unverified setup steps and any deployment limitations. A skeleton alone does not meet a request for a working feature.
