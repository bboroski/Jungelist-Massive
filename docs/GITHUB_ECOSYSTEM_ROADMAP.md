# GitHub Ecosystem Improvement Roadmap (JM-666)

**Status:** proposed, implementation tracked by PR  
**Date:** 2026-11-13  
**Scope:** all 15 currently visible repositories owned by `bboroski`  
**Operating model:** incremental, evidence-driven, repository-specific

## Mission

Build a coherent engineering ecosystem in which every repository can be understood, tested, secured, improved and released independently, while shared standards and automation reduce repetitive maintenance.

This roadmap consolidates the recent engineering discussions: the unified engineering standard, GitHub Merge Automation Standard, JM-NATIVE-66, LOVE-50 engineering principles, UTYA-ZHNETS interface/design language, NUN integration, and Jungelist Massive as the long-term language-workbench initiative.

It is a programme plan, not a claim that every proposed control or application feature already exists.

## Portfolio

The current accessible portfolio contains 15 active public repositories, all using `main` as the default branch:

- SAMBU
- ToolNG
- ReaperCripple
- Kloz
- CO
- SaintSI
- Klipot
- NUN
- NUNLauncher
- Fragile-Baby
- Luci
- Hellduck
- 9circ
- BlopScore
- Jungelist-Massive

Revalidate this inventory before each portfolio-wide batch; newly created, transferred, archived or private repositories must not be silently omitted.

## Non-negotiable engineering rules

1. Preserve each project's mission, language, architecture, public API, licence and native build/test process unless a reviewed change explicitly authorizes a change.
2. Never equate a policy document, workflow run, static check or generated preview with production readiness.
3. No force-push, default-branch deletion, protection bypass, blind conflict resolution, or mass merge.
4. Never automatically choose `ours` or `theirs` for semantic conflicts. Escalate ambiguous conflicts for human resolution.
5. Never remove dependencies, runtimes, interpreters, garbage collectors, dynamic linking or portability layers solely to satisfy an absolute optimization slogan. Measure first; retain compatibility and security.
6. Never execute untrusted pull-request code in a privileged `pull_request_target` context. Use read-only metadata there, and run untrusted tests with minimal permissions in the normal PR context.
7. Auto-merge is allowed only after a non-draft PR is mergeable, required reviews are satisfied, all required checks are complete and green, the head SHA is revalidated, and repository rules permit the selected merge method.
8. Do not delete a source branch if it is a fork branch, default branch, or referenced by another open PR.
9. Secrets stay in GitHub Actions secrets or approved secret stores; never print, commit, or expose them.
10. Every automation must have least-privilege permissions, bounded concurrency, timeouts, clear failure output and an auditable result.

## Phased execution

### Phase 0 — Inventory and baseline (Day 0–1)

- Refresh the repository inventory and default branches.
- For every repository, record language/toolchain, project purpose, README quality, licence, build/test commands, CI workflows, security alerts, rulesets, open PR count and recent release activity.
- Classify each open PR: documentation, feature, bug fix, dependency update, automation, stale, conflicting, duplicate or unsafe.
- Capture baseline metrics before changing files or settings.
- Identify repositories with no executable CI, especially 9circ as previously flagged; verify the current state before action.
- Publish a portfolio dashboard with evidence links and last-audited timestamps.

**Exit criteria:** 100% of accessible repositories inventoried; every open PR classified or explicitly marked pending review; no unverified assumptions presented as facts.

### Phase 1 — Safety and repository hygiene (Days 1–2)

- Validate `main` protection/rulesets and preserve existing valid protections.
- Review required status checks against actual workflow names; do not require checks that do not exist.
- Enable issue/PR templates, CODEOWNERS where appropriate, dependency/security update automation, and consistent labels only where they fit the repository.
- Add or validate secret scanning, dependency review and minimal-permission workflow policies where supported by the project's stack and GitHub plan.
- Ensure every repository has a concise, accurate README: purpose, status, supported platform, installation/build/test instructions, configuration, security reporting and licence.
- Avoid changing repository-wide settings until current values and permission impact are known.

**Exit criteria:** no accidental weakening of protections; every repository has a usable contribution path and documented validation commands.

### Phase 2 — CI and quality gates (Days 2–4)

- Preserve native build systems; discover commands from project files rather than guessing.
- Add a fast pull-request validation path: formatting/lint, static checks, unit tests and documentation/link checks as applicable.
- Add deeper integration, platform, performance and security jobs on appropriate schedules.
- Use dependency caching and concurrency cancellation where safe; pin third-party actions to immutable commit SHAs for hardened workflows.
- Upload test reports and build artifacts; keep logs actionable and avoid leaking secrets.
- Validate workflow YAML and scripts before enabling them as required checks.
- Treat unsupported platform/hardware tests as explicit manual gates, not fake green checks.

**Exit criteria:** every repository has at least one meaningful, passing automated validation path or a documented blocker and owner.

### Phase 3 — PR flow and controlled merge automation (Days 4–6)

Use the common pipeline:

`DISCOVER → CLASSIFY → RECONCILE → VALIDATE → REVIEW → PROMOTE → VERIFY`

- Discover all open PRs and refresh metadata immediately before acting.
- Process one eligible PR at a time per repository using FIFO ordering, with a per-repository concurrency lock.
- Detect merge conflicts and stale heads; request an update or human resolution rather than guessing.
- Re-run required checks after the final head update.
- Respect required reviews, CODEOWNERS, conversation resolution, merge queues and repository-specific merge methods.
- Activate GitHub Auto-Merge only for eligible, approved PRs with all required checks green.
- Verify the final merge commit, resulting default branch state and cleanup eligibility.
- Keep draft PRs, failing checks, unresolved conversations and ambiguous changes out of the promotion queue.

**Exit criteria:** the coordinator can explain why a PR is blocked or eligible; no PR is promoted on stale evidence.

### Phase 4 — Architecture and product improvement (Week 2 onward)

For each repository, create a project-specific technical backlog and prioritize by user value, reliability, security, maintainability and measurable performance.

- **JM-NATIVE-66:** inventory execution paths, profile hot spots, reduce avoidable overhead and consider static/native builds only when supported by the project's target profile and measurements.
- **LOVE-50:** translate the principles of care, trust, patience, fidelity and responsibility into practical product quality, documentation, humane error handling and maintainable interfaces—not decorative slogans.
- **UTYA-ZHNETS:** apply original visual tokens and reusable UI patterns only to repositories with an actual user interface; preserve each project's brand and accessibility.
- **NUN / NUNLauncher / Jungelist-Massive:** define explicit integration contracts, versioned interfaces, reproducible language-toolchain experiments and compatibility tests before cross-project coupling.
- **BlopScore and all other projects:** establish repository-specific acceptance criteria; do not infer a product role from the repository name alone.
- For performance work, record a baseline, workload, environment, before/after measurements and regression threshold.

**Exit criteria:** each feature is tied to a project requirement, acceptance tests and a rollback path.

### Phase 5 — Release engineering and continuous improvement (Week 3 onward)

- Standardize versioning and changelog conventions where appropriate.
- Add reproducible release builds, provenance/checksums and release notes.
- Run scheduled dependency, security, documentation and workflow audits.
- Track flaky tests and mean time to repair.
- Produce a weekly portfolio report with completed work, blockers, risk and next priorities.
- Retire redundant automation only after confirming no workflow or repository depends on it.

**Exit criteria:** releases are reproducible, maintenance is observable, and each cycle reduces measured technical debt.

## Priority order

| Priority | Workstream | Why it comes first |
|---|---|---|
| P0 | Inventory, branch safety, secrets, workflow permissions | Prevents accidental damage |
| P1 | Native CI, tests, PR classification | Makes future changes verifiable |
| P2 | Merge queue and guarded auto-merge | Reduces manual backlog safely |
| P3 | README, contribution docs, security and release hygiene | Makes projects operable |
| P4 | Project-specific architecture and product features | Delivers actual user value |
| P5 | Performance, native compilation and advanced automation | Optimizes against measured baselines |

## Portfolio scorecard

Track per repository and across the portfolio:

- Inventory coverage: target 100%.
- Validation coverage: target 100% of repositories have a meaningful CI path or an explicit blocker.
- Required-check reliability: successful runs / completed runs; investigate flaky checks separately.
- PR health: open count, age distribution, draft count, blocked reason and median time to merge.
- Security: unresolved critical/high findings, dependency alert age and secret-scanning incidents.
- Documentation: build/test instructions verified, README freshness and broken-link count.
- Release health: reproducibility, changelog completeness and rollback readiness.
- Performance: baseline and measured delta for every optimization claim.

Never optimize the scorecard by closing issues, weakening checks, or marking unverified work complete.

## First execution batch

1. Refresh all 15 repositories and their current PR/workflow/ruleset state.
2. Reconcile the already-open standards, merge-automation, LOVE-50, UTYA-ZHNETS and JM-NATIVE-66 PRs; avoid creating duplicate initiatives.
3. Inspect 9circ's current CI state and add a native validation workflow only after discovering its real toolchain.
4. Establish the central NUN/Jungelist Massive integration contract and roadmap ownership.
5. Start with low-risk documentation/CI fixes; keep source-level architecture changes in separate, testable PRs.

## Reporting format

Every batch report must include:

- repositories inspected / total accessible;
- changes committed and PR links;
- checks actually executed and their outcomes;
- items blocked and exact reason;
- settings changed (or explicitly not changed);
- next batch and measurable completion criteria.

**Current implementation status:** this roadmap is being introduced on a dedicated branch and must pass review and CI before it is treated as adopted policy. No mass merge, branch-protection change, production source rewrite or release is implied by this document.
