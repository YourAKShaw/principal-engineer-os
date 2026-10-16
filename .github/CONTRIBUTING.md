# Contributing

Principal Engineer OS is an agent skill package containing engineering guidance, reusable assets, and a Python validator. Start with [SKILL.md](../SKILL.md) and inspect the relevant workflow or reference before proposing a change.

For bugs, improvements, and documentation corrections, use the issue forms. Search existing issues first. Small fixes can go directly to a pull request; for broad policy or structure changes, open an issue to explain the use case and trade-offs first.

## Make a focused change

- Keep shared policy in [the constitution](../references/constitution.md); update affected workflows and assets together rather than duplicating rules.
- Scale guidance to the task. New process or complexity should have a concrete benefit.
- Use authoritative sources for technical claims and distinguish proposed evaluations from observed results.
- Keep local Markdown links relative and check that their targets exist.
- Remove credentials, private code, and personal data from examples and reports.

## Validate

From the repository root, with Python 3.9 or later:

```sh
python3 scripts/validate-skill.py
```

For changes to the validator or its wrappers, also run:

```sh
python3 scripts/test_validate_skill.py
```

The validator needs no third-party packages. It checks package structure and links; it does not prove guidance quality or agent behavior. For instruction changes, describe any representative scenario you tried, the observed result, and relevant host/model limitations. Inspect new `.github` files separately: the package validator does not validate GitHub form schemas.

## Open a pull request

Use the PR template to explain the problem, final behavior, verification, and material risks. Include related issues and report checks that were not run honestly. Keep discussion respectful and address the change rather than the contributor.
