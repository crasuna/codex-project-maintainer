---
name: codex-project-maintainer
description: "Maintain Git/GitHub projects with Codex: repository health audits, dependency updates, CI/test/build triage, release preparation, security posture checks, documentation upkeep, recurring maintenance planning, and AGENTS.md/skills/hooks/automations guidance. Use when the user asks Codex to maintain, audit, harden, release, upgrade, triage, or set up sustainable project maintenance."
---

# Codex Project Maintainer

Use this skill to help Codex keep a Git/GitHub project healthy over time. Prefer evidence from the local repository, then official documentation, then community reports only when local evidence and official sources do not explain the issue.

## Quick Start

1. Read active user, system, project, and `AGENTS.md` instructions first. Treat this skill as workflow guidance, not as permission to override higher-priority instructions.
2. Inspect the project before recommending or editing anything:
   - Git status, current branch, remotes, recent commits, and untracked files.
   - Project manifests, package manager files, tool configs, CI workflows, test/build/lint scripts, and lockfiles.
   - `README`, `LICENSE`, `CONTRIBUTING`, `SECURITY`, `CHANGELOG`, issue/PR templates, `CODEOWNERS`, release docs, and architecture or runbook docs.
3. Classify the request: health audit, routine maintenance, dependency/security update, CI failure, release preparation, documentation upkeep, or Codex automation/configuration.
4. Use `references/maintenance-reference.md` when doing a broad audit, creating sustainable maintenance policy, choosing a Codex surface, or checking security/release/GitHub baselines.
5. If changing files, identify user-owned work first. Keep edits scoped to the requested task and never mix unrelated changes into commits.
6. After changes, run the obvious available verification command(s). If none are clear, explain what was checked and what remains unverified.
7. Track unresolved errors, warnings, failed commands, and diagnostic uncertainty. Report unresolved items with source, status, impact, and next step.

## Maintenance Workflow

### Health audits

Produce an evidence-based report, not a generic checklist. Cover only areas that can be assessed from repository evidence or cited official sources:

- Project identity and scope: README clarity, install/start commands, supported platforms, license, ownership, and support policy.
- Development loop: setup, tests, lint/typecheck, build, local environment examples, dependency manager, and reproducibility.
- GitHub hygiene: CI workflows, branch protection expectations, templates, `CODEOWNERS`, Dependabot, code scanning, secret scanning, and security policy.
- Release discipline: versioning, changelog, release notes, migration notes, rollback path, package/image publishing, and supported versions.
- Security and supply chain: dependency alerts, lockfiles, SBOM/provenance posture, secret handling, vulnerability reporting, and least-privilege automation.
- Operations if relevant: configuration, logs, monitoring, SLOs, runbooks, backup/restore, incident review, and recurring maintenance cadence.

Sort findings by risk and maintenance value. For each finding, include evidence, impact, recommendation, and a concrete verification step.

### Routine maintenance

Before modifying files, determine the smallest safe maintenance batch:

- Prefer one concern per change set: dependencies, CI, docs, tests, release, security posture, or Codex setup.
- Preserve existing project conventions and tools.
- Update lockfiles only through the project package manager.
- Avoid adding dependencies unless the benefit is clear and allowed by active instructions.
- Prefer official docs for current CLI/framework behavior. Use community sources only as supporting clues and verify locally.

### CI, test, and build triage

Use three evidence lines:

1. Local evidence: exact failing command, logs, stack trace, environment, versions, and minimal reproduction.
2. Official docs: expected configuration, supported versions, migration notes, and known limitations.
3. Community feedback: issues, PRs, forums, or similar cases only when the first two lines leave a gap.

Fix the smallest proven cause. Re-run the failing command and any nearby regression checks.

### Dependency and security maintenance

Prefer safe, reviewable updates:

- Inspect advisory details and affected version ranges before upgrading.
- Separate security fixes from broad dependency refreshes unless the project already batches them.
- Run tests/build after lockfile or dependency changes.
- For public repositories, check whether `SECURITY.md`, Dependabot, code scanning, secret scanning, and dependency review are present or configured.
- For supply-chain hardening, consider SBOM, provenance, signed releases, and OpenSSF Scorecard/SLSA guidance when appropriate.

### Release preparation

Before proposing a release, verify:

- Versioning policy and package metadata are consistent.
- `CHANGELOG` or release notes cover user-visible changes.
- CI and tests pass on the release commit.
- Migration/deprecation notes exist for breaking changes.
- Rollback or re-publish behavior is documented for the project type.
- Tags, artifacts, packages, or deployment steps match existing release docs.

## Codex Surface Selection

- Use `AGENTS.md` for durable project conventions: commands, verification rules, style, commit/push policy, and review expectations.
- Use a skill for reusable cross-project workflows like this one.
- Use MCP servers, plugins, or connectors for live external data/actions such as GitHub PRs/issues, docs, monitoring, calendars, or private workspaces.
- Use hooks or rules for mechanical guardrails around tool calls, prompts, or lifecycle events.
- Use automations for scheduled maintenance, recurring dependency checks, PR follow-up, or periodic audits. Test the prompt manually before scheduling.
- Use subagents only when the user explicitly asks for parallel agents or subagent work. Prefer them for read-heavy exploration, security review, test-gap review, and log triage; be cautious with parallel write-heavy edits.

## Git and GitHub Flow

Follow active user and project instructions. When automatic commit/push is required by those instructions:

1. Confirm the target path is inside a Git worktree.
2. Confirm the repository has a GitHub remote.
3. Run obvious tests/build/lint/checks before committing.
4. Stage only files changed for this task.
5. Do not commit if tests fail, ownership of changes is ambiguous, or no GitHub remote exists.
6. Use a concise commit message that summarizes the maintenance change.
7. If push fails due to likely network issues, retry with increasing delay. If it fails due to auth, permission, non-fast-forward, branch protection, or remote rejection, stop and report the reason.

If automatic commit/push is not required, leave the worktree uncommitted unless the user asks.

## Output Shape

For audits or triage, lead with findings and risks. For completed maintenance work, summarize changed files, verification commands, and unresolved diagnostics. Keep recommendations concrete and tied to repository evidence.
