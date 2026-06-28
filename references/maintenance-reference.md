# Maintenance Reference

Use this reference only when the task needs a broad maintenance baseline, source-backed policy, or Codex surface selection. Prefer the repository's own files and active instructions for project-specific decisions.

## Source priority

1. Local evidence: repository files, command output, logs, CI output, configuration, package metadata, Git state, and reproducible behavior.
2. Official documentation: OpenAI Codex manual, GitHub Docs, language/framework/package-manager docs, NIST, OWASP, OpenSSF, SLSA, SPDX, CycloneDX, SemVer, Keep a Changelog, Google SRE, and Twelve-Factor.
3. Community feedback: issues, PRs, discussions, forums, and Q&A. Use only as a clue, then verify in the local project.

## Codex surfaces

- `AGENTS.md`: durable repository instructions. Use for project commands, verification rules, conventions, commit/push policy, and review expectations.
- Skills: reusable workflows. Use for cross-project maintenance procedures and references.
- Plugins and MCP/connectors: live external context or actions. Use for GitHub, docs, browser testing, monitoring, Figma, private apps, and workspace data.
- Hooks/rules: mechanical guardrails around lifecycle events or tool calls. Use for enforcement that should happen automatically.
- Automations: recurring scheduled work. Use for periodic audits, dependency checks, PR follow-up, and maintenance reminders.
- Subagents: explicit parallel work. Use for read-heavy scans and independent analysis; avoid unsupervised parallel edits unless the user requested that coordination.

## GitHub project health baseline

Check for:

- `README.md` with project purpose, quick start, core usage, support scope, and links to docs.
- `LICENSE` for distribution terms.
- `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, `SECURITY.md`, and `SUPPORT.md` for contributor and user expectations.
- Issue templates and PR template that request reproduction steps, environment, expected/actual behavior, risk, and verification.
- `CODEOWNERS` for review routing on sensitive or high-ownership paths.
- GitHub Actions or equivalent CI for test/build/lint/typecheck.
- Branch protection expectations: PR review, required status checks, restricted force-push/delete, and clear merge strategy.
- Dependabot version/security updates, dependency graph, dependency review, CodeQL/code scanning, secret scanning, and push protection when available.

Official anchors:

- GitHub community profiles: https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/about-community-profiles-for-public-repositories
- Issue and PR templates: https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/about-issue-and-pull-request-templates
- CODEOWNERS: https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners
- CI with GitHub Actions: https://docs.github.com/en/actions/concepts/overview/about-continuous-integration-with-github-actions
- Branch protection: https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches
- Securing a repository: https://docs.github.com/en/code-security/getting-started/quickstart-for-securing-your-repository

## Security and supply chain baseline

Use NIST SSDF as the top-level secure development model: prepare the organization, protect software, produce well-secured software, and respond to vulnerabilities. Use OWASP SAMM for maturity assessment across governance, design, implementation, verification, and operations.

Check for:

- Vulnerability intake and supported versions in `SECURITY.md`.
- Dependency update automation and lockfile discipline.
- Static analysis/code scanning appropriate to the language.
- Secret scanning or equivalent secret prevention.
- Least-privilege tokens and documented secret storage.
- Dependency review for new or changed dependencies.
- SBOM generation when users or deployment environments require inventory.
- Provenance, signed releases, or SLSA-oriented controls for higher-risk distribution.
- OpenSSF Scorecard as an external security posture signal for open source projects.

Official anchors:

- NIST SSDF SP 800-218: https://csrc.nist.gov/pubs/sp/800/218/final
- OWASP SAMM: https://owaspsamm.org/model/
- OpenSSF Scorecard: https://openssf.org/projects/scorecard/
- OpenSSF Best Practices Badge: https://openssf.org/projects/best-practices-badge/
- SLSA: https://slsa.dev/spec/v1.2/about
- SPDX specifications: https://spdx.dev/use/specifications/
- CycloneDX specification: https://cyclonedx.org/specification/overview/

## Release and compatibility baseline

Check for:

- Versioning policy, preferably SemVer for libraries/packages where compatibility matters.
- Human-readable changelog organized by version.
- Release notes that separate breaking changes, features, fixes, security, and migration notes.
- Reproducible build/publish commands.
- Clear support window for maintained versions.
- Rollback or remediation path for bad releases.
- Tagged releases and artifacts that match existing project conventions.

Official anchors:

- Semantic Versioning: https://semver.org/
- Keep a Changelog: https://keepachangelog.com/en/1.1.0/

## Operations and sustainability baseline

For services or tools with operational responsibility, check for:

- Configuration separated from code and documented through examples such as `.env.example`.
- Reproducible setup and parity between development, CI, and production where practical.
- Structured logs and actionable errors.
- Metrics or health checks for critical paths.
- SLI/SLO definitions when reliability commitments exist.
- Runbooks for common failures, deployment, rollback, backup, and restore.
- Incident or maintenance review cadence.

Official anchors:

- Twelve-Factor App: https://www.12factor.net/
- Google SRE service level objectives: https://sre.google/sre-book/service-level-objectives/

## Maintenance cadence

Use this as a default starting point and adjust to project risk:

- Weekly: triage issues/PRs, review CI failures, close stale noise carefully.
- Biweekly: merge safe dependency updates, refresh small docs drift, address flaky tests.
- Monthly: review security alerts, slow tests, build times, release backlog, and high-value maintenance debt.
- Quarterly: reassess roadmap, architecture decisions, supported versions, permissions, automations, and supply-chain posture.
- Before every release: run release checklist, verify changelog/release notes, check dependency/security alerts, and document rollback.

## Audit output template

Use this compact shape unless the user asks for a different format:

```md
## Findings
- [Severity] Area: concise issue
  Evidence: file/command/source.
  Impact: why it matters.
  Recommendation: concrete action.
  Verification: command or observable result.

## Strengths
- Existing practices worth preserving.

## Suggested next batch
- 3-5 scoped maintenance tasks in recommended order.

## Unresolved diagnostics
- Only include unresolved failures, warnings, or uncertainty.
```
