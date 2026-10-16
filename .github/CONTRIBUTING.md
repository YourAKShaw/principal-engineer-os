<div align="center">

# 🤝 Contributing to Principal Engineer OS

**Help make engineering judgment clearer, more useful, and easier to verify.**

[![PRs Welcome](https://img.shields.io/badge/PRs-Welcome-2563EB?style=flat-square)](https://github.com/YourAKShaw/principal-engineer-os/pulls)
[![Python 3.9+](https://img.shields.io/badge/Validator-Python%203.9%2B-334155?style=flat-square)](../scripts/validate-skill.py)
[![License: MIT](https://img.shields.io/badge/License-MIT-2563EB?style=flat-square)](../LICENSE)

[Project overview](README.md) · [Skill entry point](../SKILL.md) · [Get help](SUPPORT.md)

</div>

---

## Start with the engineering problem

Principal Engineer OS is an agent skill package containing a shared engineering constitution, focused workflows, domain guidance, reusable artifacts, and a Python validator. Contributions should improve the decisions an agent makes and the evidence it provides.

Useful contributions include:

- A realistic failure case the guidance currently misses.
- A clearer rule for authorization, data integrity, compatibility, or recovery.
- A simpler workflow that preserves the important engineering checks.
- A better example, template, local link, or package validation check.
- A behavioral evaluation that reports observed results and limitations.

Read [SKILL.md](../SKILL.md), [the constitution](../references/constitution.md), and the affected workflow or reference before changing guidance.

## 🧭 Choose the right starting point

| Contribution | Where to begin |
| :--- | :--- |
| Small correction or focused fix | Open a pull request with the problem and verification. |
| Bug, missing guidance, or documentation issue | Search existing issues, then use the matching [issue form](https://github.com/YourAKShaw/principal-engineer-os/issues/new/choose). |
| Broad policy or package structure change | Open an issue first with the use case, trade-offs, and proposed scope. |
| Usage question | Follow the [support guide](SUPPORT.md). |

Use sanitized examples. Remove credentials, private code, personal data, and sensitive vulnerability details before posting publicly.

## Make a focused change

1. Fork the repository and create a branch for your change.
2. Inspect the relevant guidance and its linked workflows or assets.
3. Make the smallest coherent update that addresses the problem.
4. Validate the package and inspect the complete diff.
5. Open a pull request describing the final change and its evidence.

### Keep the package coherent

| Principle | What to preserve |
| :--- | :--- |
| **One shared policy** | Keep common rules in [the constitution](../references/constitution.md). Update affected workflows and assets together rather than creating competing copies. |
| **Proportional effort** | Give new process or complexity a concrete benefit. Tiny changes should remain easy to complete. |
| **Evidence over assertion** | Use authoritative sources for technical claims. Separate proposed evaluations from executed checks and observed results. |
| **Focused resource loading** | Put domain detail in the relevant reference and keep entry-point routing clear. |
| **Explicit scope and authority** | Preserve the distinctions between discovery, design, review, implementation, and operations. |
| **Usable documentation** | Keep local Markdown links relative, verify their targets, and make examples self-contained enough to follow. |

## 🔍 Validate your change

From the repository root, with **Python 3.9 or later**:

```sh
python3 scripts/validate-skill.py
```

The validator requires no third-party packages. It checks the package manifest, required resources, local links and anchors, reachability, and empty or unfinished package files.

Alternative wrappers:

```sh
sh scripts/validate-skill.sh
```

```powershell
powershell -File scripts/validate-skill.ps1
```

For changes to the validator or its wrappers, also run the regression suite:

```sh
python3 scripts/test_validate_skill.py
```

**Package checks and behavioral evidence answer different questions.** Passing the validator does not establish engineering quality or agent behavior. Inspect `.github` changes separately: the package validator does not validate GitHub form schemas or these documentation pages.

### When you change instructions

Describe a representative scenario, the relevant host/model and available tools, what the agent actually did, and any remaining limitations. A tiny correction may need only contextual inspection; a consequential policy change benefits from a scenario that exercises the affected boundary.

Useful scenarios include a tenant authorization review, a payment timeout with an uncertain outcome, a rolling migration, a measured performance issue, or a malicious retrieved document. Compare against a baseline when making comparative claims, and report only results you observed.

## 📬 Open a reviewable pull request

Use the [pull request template](pull_request_template.md) to explain:

- **Problem and outcome:** what failed or was unclear, and what the change improves.
- **Scope:** affected guidance, workflows, assets, or validator behavior, with related issues.
- **Verification:** exact commands and results, plus relevant scenario observations.
- **Risks and limits:** unresolved trade-offs, compatibility implications, and checks not run.

Keep the diff focused and the discussion respectful. Address the change rather than the contributor, and use concrete examples when explaining a disagreement.
