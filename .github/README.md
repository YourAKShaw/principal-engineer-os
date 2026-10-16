# GitHub contribution files

This directory lives at the repository root. It contains:

| File | Purpose |
| --- | --- |
| `ISSUE_TEMPLATE/*.yml` | Structured bug, improvement, and documentation forms. |
| `ISSUE_TEMPLATE/config.yml` | Issue chooser configuration; keeps blank issues available for questions and unusual reports. |
| `pull_request_template.md` | A single default PR description with scope, verification, and risk prompts. |
| [CONTRIBUTING.md](CONTRIBUTING.md) | Contribution workflow and actual package validation commands. |
| [SUPPORT.md](SUPPORT.md) | Usage and support routing. |

Forms deliberately avoid automatic labels and assignees so they do not depend on separately configured repository metadata. Templates become available through GitHub after they reach the default branch.

## Other common GitHub files

Add these when their prerequisites and policies are decided:

- `DISCUSSION_TEMPLATE/<category-slug>.yml`: discussion forms require Discussions and matching categories; they cannot be used for announcement categories.
- `SECURITY.md` and `VULNERABILITY_REPORT.yml`: document a working private reporting channel before inviting sensitive reports. A custom vulnerability form also requires private vulnerability reporting to be enabled.
- `CODE_OF_CONDUCT.md`: adopt a conduct policy with an actual enforcement contact and process.
- `CODEOWNERS`: assign review ownership once maintainers and review boundaries are decided.
- `FUNDING.yml`: add verified sponsorship accounts when applicable.
- `workflows/*.yml` and `dependabot.yml`: automation configuration, rather than contributor templates; add for the project's actual CI and dependency needs.

Multiple PR templates are possible, but selecting them requires links with a `template` query parameter. One default keeps routine contributions straightforward.

## References

- [GitHub issue and pull request templates](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/about-issue-and-pull-request-templates)
- [Issue form syntax](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/syntax-for-issue-forms)
- [Community health files](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file)
- [Discussion category forms](https://docs.github.com/en/discussions/managing-discussions-for-your-community/creating-discussion-category-forms)
