# Global Ecosystem Federation Blueprint

**Program:** JUNGELIST MASSIVE / JM-SPACE-50  
**Program coordinator:** Jungelist Massive  
**Existing architecture/manifest authority:** SAMBU  
**Scope:** 15 repositories under `bboroski`  
**Status:** Initial architecture baseline; implementation claims remain evidence-gated  
**Updated:** 2026-11-13

## 1. Mission

Create a federated engineering ecosystem in which every repository can discover, consume, validate, and contribute reusable capabilities without erasing project identity or creating an unsafe universal runtime.

This is a federation, not a source-code blender. A capability is shared through a versioned API, schema, library, adapter, build artifact, or documented workflow. Source code is not copied between projects merely to make repositories look uniform.

## 2. Control-plane responsibilities

- **Jungelist Massive:** cross-project roadmap, language research, integration proposals, and acceptance criteria; it coordinates work but does not supersede existing architecture authority.
- **Klipot:** operator-facing repository catalog, dependency graph presentation, contract catalog, and status portal.
- **Hellduck:** integrated workspace for its six source modules, migration verification, and workspace-level checks.
- **Luci:** engineering-domain taxonomy and policy validation foundation.
- **SAMBU:** current authority for shared module-manifest conventions, canonical module registry, and ecosystem architecture; its language and scientific-modeling platform remains independently owned.

These roles are complementary. SAMBU remains the current authority for shared architecture and module-registry semantics; Klipot presents registry data; Hellduck federates workspace views; Jungelist Massive coordinates cross-project proposals. Any change to that authority requires an explicit reviewed governance decision.

## 3. Repository federation map

| Repository | Primary domain | Integration posture |
|---|---|---|
| SAMBU | Language/runtime and scientific modeling | Provider of language tooling and manifest conventions; Python-hosted workflows remain distinct from native firmware |
| ToolNG | Windows-native device diagnostics | Consume selected policy concepts through native C adapters; preserve read-only device boundary |
| ReaperCripple | Embedded BSP, firmware, calibration | Consume optional platform/lifecycle/assurance adapters only through explicit target contracts |
| Kloz | Freestanding platform substrate | Provider of versioned platform operations and caller-owned memory contracts |
| CO | Deterministic component lifecycle | Provider of bounded lifecycle state machine; optional Kloz context bridge |
| SaintSI | Runtime assurance observer | Provider of bounded health observations; no implicit reset or actuator authority |
| Klipot | Ecosystem portal/control plane | Provider of discovery, registry projection, and contract presentation |
| NUN | Early x86_64 kernel substrate | Owns kernel, boot, memory, and execution contracts; no arbitrary user-space module injection |
| NUNLauncher | Kernel-image admission | Validates versioned image metadata and handoff prerequisites; does not execute or authenticate unsigned images |
| Fragile-Baby | Elbrus/E2K platform qualification | Evidence workstream; no target capability claim without exact hardware/toolchain evidence |
| Luci | Engineering control plane and policy catalog | Provider of local policy/domain validation; no universal autonomous executor |
| Hellduck | Six-module engineering workspace | Workspace snapshot and migration verification; source repositories retain their own history and releases |
| BlopScore | Native Windows hardware-inspection application intent | Architecture and implementation evidence must be established before runtime integration |
| 9circ | Unclassified project | Discovery-only until purpose, source, license, build, and ownership are documented |
| Jungelist-Massive | Ecosystem architecture and language foundry | Federation coordinator; must remain independently buildable and must not absorb other projects |

## 4. Layered architecture

Use layers as explicit contracts, not as a mandatory directory template:

1. **L0 — Hardware and platform:** CPU/SoC, board revisions, firmware, host OS, device-specific facts.
2. **L1 — Platform primitives:** memory, time, status codes, capabilities, device and execution boundaries.
3. **L2 — Runtime and lifecycle:** bounded component lifecycle, scheduling assumptions, fault retention, resource ownership.
4. **L3 — Assurance and security:** evidence, integrity checks, trust decisions, permission boundaries, provenance.
5. **L4 — Domain services:** diagnostics, language tooling, scientific models, calibration, image admission.
6. **L5 — Applications and interfaces:** desktop applications, CLIs, portals, operator tools.
7. **L6 — Federation/control plane:** repository catalog, schemas, compatibility matrix, roadmap, integration evidence.

Each project implements only the layers it owns. Cross-layer calls must pass through versioned interfaces. Kernel, firmware, desktop, browser, and Python-hosted components are not interchangeable runtimes.

## 5. Integration rules

- Every shared module has a stable identifier, semantic version, license, supported targets, API/schema version, provenance, and verification evidence.
- Dependencies are explicit and directional. Optional adapters remain optional; avoid cycles.
- Consumers pin a compatible version or immutable artifact digest. Floating branches are not release dependencies.
- Compatibility is checked before adoption; deprecation requires a documented migration window.
- Each repository remains independently buildable and testable.
- A registry entry describes a capability; it does not prove that code is integrated, executable, secure, or production-ready.
- Cross-repository data is minimized. Secrets, private user data, and unrelated personal information are never copied into manifests or logs.
- Imported repository content is untrusted data until reviewed, licensed, scanned, and tested.

## 6. Native-build doctrine — qualified per project

Prefer native machine-code delivery, static linking, deterministic memory ownership, reproducible builds, and a single deployable artifact **where the target and project architecture support them**.

Do not force this preference onto:
- Python-hosted SAMBU workflows or browser-based Klipot;
- NUN's freestanding kernel and boot-image boundaries, which have their own link and image contracts;
- toolchains/platforms that require dynamic system libraries or shared runtime services;
- projects whose current verified implementation is not yet a native application.

No blanket removal of interpreters, dynamic libraries, or virtual machines is authorized by this blueprint. Such changes require a project-specific architecture decision, dependency audit, size/performance evidence, and rollback plan.

## 7. Required integration lifecycle

1. **Discover:** inspect repository, purpose, source tree, license, build, tests, workflows, dependencies, and security boundary.
2. **Classify:** identify owned layers, exported capabilities, consumed contracts, maturity, and unknowns.
3. **Specify:** add or update a versioned manifest and interface contract.
4. **Adapt:** implement the smallest project-native adapter; do not transplant unrelated source trees.
5. **Verify:** run local tests, consumer/provider contract tests, build checks, static analysis, and target-specific validation.
6. **Propose:** open a focused PR with diff, evidence, risks, migration, and rollback.
7. **Promote:** merge only after required human review and passing repository checks.
8. **Observe:** publish integration status and compatibility results to Klipot/Hellduck without claiming unperformed checks.

## 8. Adoption waves

### Wave A — Inventory and contracts
- Complete purpose/build/license/maturity inventory for all 15 repositories.
- Reconcile the SAMBU canonical module registry with Klipot and Hellduck; treat the JM inventory as a coordination snapshot.
- Add missing manifests only after project owners and contracts are confirmed.
- Resolve unknown project scope for 9circ and implementation maturity for BlopScore.

### Wave B — Shared primitives
- Validate the Kloz platform ABI and CO lifecycle adapter boundaries.
- Validate SaintSI observation semantics and ReaperCripple's optional adapters.
- Establish artifact provenance, version pinning, compatibility tests, and reproducible build metadata.

### Wave C — System and application integration
- Validate NUN ↔ NUNLauncher boot-image contracts.
- Keep Fragile-Baby E2K qualification evidence separate from x86_64 assumptions.
- Connect ToolNG and BlopScore only through documented, least-privilege Windows interfaces.
- Connect SAMBU/Jungelist language tooling through versioned language and artifact interfaces.

### Wave D — Federation operations
- Publish a single ecosystem graph in Klipot, sourced from canonical manifests.
- Use Hellduck as a workspace verification surface, not as a replacement for source repositories.
- Use Luci for policy metadata and local validation, not as an unbounded executor.
- Make JM roadmap changes evidence-based and reviewable.

## 9. Acceptance criteria

- [ ] All 15 repositories are represented with accurate purpose, owner, default branch, license, maturity, and manifest status.
- [ ] Every dependency is directional, versioned, and backed by an actual interface.
- [ ] No unreviewed source copying or runtime coupling is introduced.
- [ ] Each repository's existing build/test/security workflows remain authoritative.
- [ ] Contract tests exist for every claimed implemented integration.
- [ ] Native-build claims match actual artifacts and target evidence.
- [ ] Klipot and Hellduck consume the SAMBU canonical registry semantics; JM publishes a linked coordination snapshot.
- [ ] Unknown, planned, partial, and implemented states are distinguishable.
- [ ] Rollback and deprecation procedures are documented.
- [ ] No branch protection, secrets, releases, deployments, or destructive operations are changed without explicit repository-level authorization.

## 10. Status vocabulary

- `implemented`: source code and relevant tests demonstrate the capability.
- `partial`: a bounded subset exists; missing parts are stated.
- `planned`: design or roadmap only.
- `blocked`: a dependency, permission, toolchain, or evidence gap prevents progress.
- `unverified`: source or metadata suggests a capability, but required evidence was not run or is unavailable.

## 11. First execution backlog

1. Inspect and reconcile the Klipot registry, Hellduck contracts, and SAMBU manifests.
2. Align with the existing SAMBU manifest/registry schema and add a compatibility test fixture; do not create a competing canonical schema.
3. Add accurate manifests for repositories that lack one; do not invent missing project details.
4. Add provider/consumer contract tests for each real integration edge.
5. Establish a per-repository build/test matrix and artifact provenance.
6. Publish the integration graph and status report.
7. Expand the roadmap only from measured gaps and verified improvements.

---
This blueprint is an architecture proposal and coordination baseline. It does not assert that all integrations, native builds, target tests, or production deployments have already been implemented.
