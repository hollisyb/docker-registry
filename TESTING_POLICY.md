# Tiered Test Execution Policy

Status: **NORMATIVE / PROJECT ADOPTION**

Canonical cross-project source: `hollisyb/home-ai-lab` commit `65fce7d20cb8578a62c2219f3d6cb893008085dd`, `docs/operations/tiered-testing-policy.md`.

This repository adopts that policy. A stricter repository-specific safety, release, or acceptance rule takes precedence.

## Required cadence

1. **Routine development / small fixes:** run targeted tests for the changed code and immediate contracts. Do not pause development merely because a push automatically started the repository Full Suite.
2. **Completed functional slice:** run the affected module test set and relevant integration tests.
3. **PR Ready / key milestone:** run the repository Full Suite as the formal acceptance gate and use exact final-head evidence.
4. **Substantive executable change after that evidence:** rerun the Full Suite on the new final head before merge. Documentation-only or clearly non-executable changes do not require another Full Suite unless repository protection requires it.
5. **After merge:** when a repository-wide integration suite exists, run or observe one post-merge Full Suite on the exact default-branch merge SHA.

Material changes to authorization, fail-closed behavior, security/permissions, destructive data handling, backup/restore/migration/recovery, shared runtime infrastructure, repository-wide contracts, or production/Runtime GO conditions may be escalated directly to key-milestone / Full-Suite testing regardless of code size.

Never weaken production validation, authority checks, warning policy, fail-closed behavior, or test expectations merely to make CI green. Do not hide unexplained failures with skips, xfail, warning filters, retries, or environment relaxation.

Default sequence:

`targeted tests -> module/slice tests -> PR Ready Full Suite -> merge -> post-merge Full Suite`

Avoid the anti-pattern:

`small edit -> wait for Full Suite -> small edit -> wait for Full Suite -> ...`
