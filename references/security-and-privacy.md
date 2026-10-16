# Security and privacy engineering

Use when trust boundaries, identity, permissions, sensitive data or execution privileges change. Contents: threat model; identity; authorization; input/egress; secrets; supply chain; verification and privacy.

## Model the changed boundary

Identify assets/classification, actors and privileges, entry points, data flows/stores, external dependencies, attacker capabilities, abuse cases and existing controls. For each meaningful threat record impact, likelihood, enforcement point, negative test, residual risk and owner. STRIDE is a useful prompt, not a substitute for domain analysis.

An ordinary feature may need a focused boundary review rather than a formal security audit. Never infer a vulnerability solely from a library name or scanner count. Establish reachability and a plausible attack path.

## Identity and sessions

Use established identity systems and protocols instead of custom cryptography. Verify issuer, audience, signature/allowed algorithms, expiry and intended token use. JWT presence does not establish permission. Use appropriate short lifetimes, rotation and revocation; secure refresh credentials and recovery flows.

For password-based systems, use a maintained adaptive hashing implementation with current parameters (for example Argon2id), and assess reset/account-recovery abuse. Privileged or high-risk actions may need MFA and step-up authentication. In browsers, choose Secure/HttpOnly/SameSite cookies and CSRF protection based on actual request semantics. Verify current provider and platform guidance before implementation.

## Authorization and tenant isolation

Enforce explicit permission and ownership checks at privileged server-side operations, including background jobs, exports and admin paths. Default deny. Select RBAC, ABAC or relationship-based permissions from domain needs rather than fashion.

Derive tenant identity from trusted authentication or verify any selected tenant against it. Scope object lookups and writes, search indexes, cache keys and async payloads. Database row-level security may add defense in depth; it does not excuse missing use-case policy. Recheck time-sensitive authority when a queued job executes.

Test horizontal and vertical escalation: change object IDs, tenant fields, role fields, nested resources, job payloads and export parameters. Test revoked membership, stale sessions and denial when the policy dependency fails. Client-side hiding is UX, never enforcement.

## Parse, bound and encode

- Parameterize SQL values; allowlist dynamic identifiers and order clauses. Do not mistake escaping for parameterization.
- Encode output for HTML, JavaScript, URL or other destination context. If rich HTML is required, use a maintained sanitizer with a deliberate policy.
- Bound body/file size, nesting, cardinality, decompression, recursion and expensive filter work. Validate external JSON at runtime; reject mass assignment of privileged fields.
- Prevent traversal in file paths and archive extraction, unsafe deserialization and applicable XML external entities. Check uploaded content beyond filename extensions; quarantine/scan where needed.
- For SSRF, constrain destinations and schemes with controls appropriate to redirects, DNS and the actual HTTP client. Validate outbound access at the execution boundary; do not rely solely on model instructions or a naive string check.
- Invoke subprocesses with argument arrays and narrow capabilities. Never interpolate untrusted input into shell commands.
- Verify webhooks with the provider's actual signature protocol, enforce freshness/replay policy and make effects idempotent.

Choose TLS, HSTS, CSP, CORS, CSRF, clickjacking protections, safe content types, rate limits and bot/abuse controls from the threat model. CORS does not authorize server operations. Errors should not reveal sensitive internals or account/resource existence when that increases risk.

## Secrets, telemetry and execution

Use approved secret injection/management and least-privilege service identities, with separate environments, rotation and controlled key lifecycles. Keep credentials out of source, images, logs, traces, screenshots, examples and model inputs. Protect backup and infrastructure state, which can contain secrets.

If a secret was exposed, revoke/rotate, assess scope and preserve necessary incident evidence; deleting the latest line does not eliminate history or downstream copies. Do not print secret values while investigating them.

Give CI, agents and tools the minimum file, network and account permissions. Review untrusted scripts and install hooks before execution. Do not send repository data to an unapproved endpoint, execute opaque remote installers, disable controls to pass tests, or bypass branch/environment protection.

## Supply chain and verification

Review direct/transitive dependency purpose, maintenance, advisories, license compatibility, install scripts and upgrade path. Pin or lock reproducibly as appropriate. Protect build runners and registries, scope publication tokens, and use provenance/signatures/SBOMs when release obligations require them. Avoid exposing secrets to untrusted pull-request code.

Select threat-driven tests: access bypass, tenant crossover, injection, replay, expired/revoked sessions, forged webhooks, upload abuse, quotas and leaks through error/telemetry paths. Complement these with relevant SAST, dependency, secret, IaC/container and dynamic scans. A clean scanner result is evidence about its checks, not proof of safety.

Maintain vulnerability reporting, triage by impact/likelihood, patch timelines, auditable privileged operations and incident escalation. Separate confirmed vulnerabilities from hypotheses needing authorized investigation.

## Privacy and compliance scope

Map collection, purposes, processors, residency, access and propagation. Minimize personal data and define retention, deletion/export and subject-rights behavior where applicable. Include prompt/evaluation data and telemetry. Handle legal holds and backup retention honestly; do not promise instantaneous deletion from every copy without evidence.

For regulated work, determine the applicable jurisdiction/product obligations with qualified input, map controls to requirements, record owners and protect evidence. Following PEOS, OWASP or a cloud checklist does not establish certification or legal compliance.

## Foundations

[NIST SSDF](https://csrc.nist.gov/projects/ssdf/publications), [OWASP ASVS](https://owasp.org/www-project-application-security-verification-standard/), [OWASP API Security](https://owasp.org/API-Security/), [OWASP Cheat Sheets](https://cheatsheetseries.owasp.org/), [OpenSSF Best Practices](https://www.bestpractices.dev/), [SLSA](https://slsa.dev/). Adapted from master §§4, 14 and 24. Check adopted versions and applicability before claiming a control requirement.
