# Multi-Axis Layer Architecture

**Architecture:** NUN Mesh — Multi-Axis Layer Fabric (MALF)  
**Repository:** `bboroski/Jungelist-Massive`  
**Role:** Proposed desktop workbench for designing and generating new programming languages  
**Maturity:** Repository shell with placeholder README; product architecture is proposed and not implemented.  
**Status:** Proposed target architecture; no capability is considered implemented without source and test evidence.

## Purpose

MALF defines multiple independent axes: structural layers, vertical user journeys, trust boundaries, lifecycle stages and assurance planes. It is not permission to add a heavyweight framework or move code without measurable value.

## Structural layers

| ID | Layer | Responsibility |
|---|---|---|
| L0 | **Experience** | Desktop UI, CLI and operator workflows. |
| L1 | **Contracts** | Public APIs, schemas, project manifests, plugin descriptors and events. |
| L2 | **Application orchestration** | Use cases, workflows, command dispatch and lifecycle sequencing. |
| L3 | **Domain kernel** | Core domain models, deterministic algorithms and product invariants. |
| L4 | **Policy and capabilities** | Permissions, safety gates, trust, budgets and operation allowlists. |
| L5 | **Ports and contracts** | Abstract OS, hardware, compiler, storage and provider interfaces. |
| L6 | **Adapters and platform** | Concrete native OS, device, compiler and external-source implementations. |
| L7 | **State and artifacts** | Project state, configuration, registries, generated output and provenance. |
| L8 | **Runtime and delivery** | Build, packaging, deployment, process isolation and runtime composition. |
| L9 | **Assurance and evidence** | Tests, benchmarks, compatibility and target-qualification evidence. |

## Dependency law

- L0 invokes L2 use cases via L1 contracts; UI widgets do not contain domain/compiler/device policy.
- L2 coordinates L3 domain rules and L4 policy through L5 ports.
- L6 implements L5; the domain does not depend on a concrete OS, driver, compiler vendor or remote service.
- L7 is accessed through explicit repositories and versioned formats.
- L8 composes and isolates execution; inner layers do not assume a particular deployment environment.
- L9 verifies user-visible behavior, boundaries, resource limits and compatibility.

**Allowed:** UI/CLI → application → domain/policy → port → adapter → observable result.  
**Forbidden:** UI directly invoking privileged hardware/compiler effects; domain importing native APIs; unreviewed plugin code running in-process.

## Orthogonal architecture axes

1. **Structural:** L0–L9 ownership.
2. **Vertical slices:** complete journeys from user intent through domain decision, adapter, saved artifact and tests.
3. **Trust:** user input → parse/normalize → validate → policy/capability gate → bounded execution → provenance record.
4. **Lifecycle:** design → configure → build → test → package → install/run → update → rollback/uninstall.
5. **Assurance:** tests, telemetry, benchmarks and target evidence remain separate and are linked to exact builds.

## Repository-specific allocation

### L0 — Language foundry workspace
Proposed desktop IDE with project navigator, grammar editor, semantic model viewer, pipeline graph, diagnostics and generated-language preview.

### L1 — Language and plugin contracts
Versioned language project format, grammar schema, AST/IR schemas, compiler backend ABI, extension manifest and diagnostic protocol.

### L2 — Foundry orchestration
Create language project → validate specification → generate grammar/parser scaffolding → run conformance tests → build compiler/runtime package.

### L3 — Language design domain
Language identity, syntax/grammar, type system, semantics, module system, memory model, concurrency model and interoperability rules.

### L4 — Generation and execution policy
Deterministic generator rules, capability declarations, resource budgets, untrusted-extension policy and explicit distinction between generated and verified artifacts.

### L5 — Compiler construction ports
Abstract lexer/parser generators, semantic passes, IR transforms, optimization passes, code generators, debuggers and test runners.

### L6 — Compiler and toolchain adapters
Concrete native toolchains, VM/interpreter targets, transpilers, external compiler integrations and language-specific runtimes behind adapters.

### L7 — Language projects and artifacts
Versioned language specifications, grammar sources, test corpus, generated source, binaries, package metadata and reproducibility records.

### L8 — Desktop/runtime delivery
Native desktop packaging, isolated build workers, plugin boundaries, toolchain discovery, cache and cross-platform distribution.

### L9 — Language conformance and compiler assurance
Grammar tests, parser fuzzing, type/semantic conformance, IR verification, differential backend tests, reproducible builds and performance benchmarks.

## Vertical slices

1. **Create a new language:** User intent → structured language spec → grammar/type/semantic validation → generated frontend → conformance fixtures → versioned project.
2. **Compile a sample program:** Source → lexer/parser → AST → semantic analysis → typed IR → verified transforms → backend adapter → artifact and diagnostics.
3. **Add a new backend:** Versioned backend contract → capability declaration → adapter implementation → differential tests → package compatibility gate.
4. **Extension ecosystem:** Extension manifest → trust/provenance check → permission review → isolated worker → bounded execution → audit record.

## Cross-cutting planes

- **Security:** least privilege, explicit user consent for elevated actions, secret hygiene and deny-by-default extension loading.
- **Isolation:** treat plugins, generated programs and external toolchains as untrusted until constrained and verified.
- **Reliability:** bounded memory, CPU, process lifetime and output size; explicit cancellation and recovery.
- **Compatibility:** version project files, manifests, plugin APIs and generated artifact metadata.
- **Observability:** record input identity, toolchain/version, output hash, duration and failure reason without leaking secrets.
- **Accessibility:** keyboard-first operation, readable status, contrast and reduced-motion support.
- **Performance:** profile native user paths and real target workloads before optimizing.

## NUN Mesh federation

Shared manifests and integration references are metadata contracts only. A repository registry must never imply a plugin is trusted, executable or compatible. External tools and projects are accessed only through versioned adapters and explicit user-controlled capabilities.

## Incremental adoption

1. Map current files (if any) and mark absent components as proposed, not implemented.
2. Freeze product scope, public contracts and project-file schemas.
3. Implement one vertical user journey from input to verified output.
4. Keep domain and compiler logic separate from UI and OS-specific adapters.
5. Add policy gates before native, hardware, process or plugin effects.
6. Persist outputs with provenance and reproducible metadata.
7. Add L9 tests and build/package gates before adding more feature surface.
8. Refactor only when a layer boundary reduces real coupling or improves testability.

## Definition of done

A feature has a user story, owning layer, versioned contract, explicit threat/permission model, deterministic failure behavior, test coverage and reproducible evidence. Proposed architecture is never presented as shipped functionality.

## Repository guardrails

Treat all compiler backends, generated programs and extensions as untrusted until validated and isolated. Do not start by promising arbitrary automatic creation of production-ready languages. First ship a deterministic language-spec model, validator and one vertical compiler pipeline with tests. Never execute generated code in the desktop process by default.
