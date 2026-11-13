# Jungelist Massive — OMEGA native studio design and implementation contract

**Product:** Jungelist Massive  
**Specification lineage:** 7.7.7-OMEGA  
**Status:** Proposed implementation contract; the SVG is a static design concept, not a running application.

## 1. Product definition

Jungelist Massive is a native language-design workbench. The Massive Knob edits a deterministic, inspectable language profile. It does not directly mutate compiler code or silently invent semantics. Every generated artifact is reproducible from a versioned profile, seed, generator version and target capability set.

## 2. Primary workspace

- Top command rail: project, profile, undo/redo, target, build state and export.
- Macro encoder: rotary control, numeric value entry, keyboard increments, five zone ranges and visible lock state for discrete transitions.
- Language profile: syntax density, semantic strictness, computation model, evaluation strategy, memory model and effect policy.
- Workbench tabs: Lexicon, Grammar, Types, Semantics, IR, Codegen, Transpiler and Runtime.
- Editor: syntax highlighting, diagnostics, source map, generated examples and compiler output.
- Inspector: provenance, seed, profile hash, generator versions, target features and validation status.
- Performance HUD: frame-time percentiles, CPU/GPU timings, memory, queue depth and benchmark environment. Never show fabricated FPS or latency.
- Export center: CLI, LSP, editor extension, stdlib and reproducibility manifest, each with its own readiness state.

## 3. Visual language

Use near-black graphite as the structural foundation. Acid yellow marks the active macro value and primary action; cyan marks dataflow and generated artifacts; magenta is reserved for experimental or unverified modes. Keep surfaces flat and layered by tonal contrast, with fine grid lines and restrained waveform/step motifs. Avoid decorative neon that competes with code or diagnostics.

Typography: Inter/Segoe UI for interface labels; JetBrains Mono/Cascadia Code for code, IDs and measurements. Use tabular numerals for theta, timings and benchmark values. Controls have generous hit areas; the rotary knob supports pointer, touch, keyboard and direct numeric input.

## 4. One-Knob behavior

The knob maps theta in [0, 1] to a versioned profile through documented transfer functions. The mapping is deterministic for the tuple:
(profile_schema, generator_version, seed_256, theta, target_capabilities).

- Hermite curves are bounded and monotonic where required.
- Hysteresis is explicit for discrete architecture transitions and has deterministic tie-breaking.
- Every parameter exposes its derived value, source curve, constraints and whether it was user-overridden.
- Randomness is seeded and replayable; no hidden entropy enters a build.
- Undo/redo stores profile snapshots, not opaque UI deltas.
- Zone labels are descriptive presets, not guarantees of type soundness or runtime behavior.

## 5. Compiler pipeline and truthful capability states

profile → lexicon → grammar → parser → type checker → semantic validation → HIR → MIR → backend → artifact

Keep each stage as a separately testable Rust crate or module with versioned input/output schemas. Use a stable intermediate representation and diagnostics contract. A backend is selectable only when its dependency, target and tests are present.

| Capability | Acceptance evidence |
|---|---|
| Grammar synthesis | Generated EBNF/PEG, ambiguity tests, parser round-trip fixtures |
| Type system | Inference tests, negative fixtures, soundness argument for the supported subset |
| Z3 integration | Version-pinned solver adapter, bounded queries, timeout/unknown handling, reproducible SMT-LIB fixtures |
| Cranelift JIT | Executable generated code, sandbox boundary tests, trap/timeout tests |
| LLVM AOT | Target-specific object output, linker integration and ABI tests |
| wgpu UI | Adapter/device fallback, GPU timing, software fallback and frame-time measurements |
| LSP | Protocol conformance, cancellation, incremental sync and editor integration tests |
| Transpiler | Golden corpus with semantic equivalence checks, not text-only similarity |

A solver result of UNKNOWN is not proof. A successful parse is not proof of type soundness. A generated binary is not proof of sandbox safety.

## 6. DUB-FLUX 58% profile

Store the example as a fixture with its seed, profile hash, grammar version and expected diagnostics. Validate stack effects statically. The supplied Fibonacci and IO example is illustrative until the parser, stack-effect checker, IO effect typing and execution tests pass. The UI must not present it as executable merely because it appears in the editor.

## 7. Performance budgets

Measure interaction-to-visible-update latency at p50/p95/p99, not just average FPS. Separate UI rendering, profile recomputation, grammar generation, type checking and JIT compile time. Use cancellation and stale-result suppression for background work. A 120/240 Hz target is device-dependent, not a universal promise.

## 8. Accessibility and quality

- Full keyboard operation for knob, tabs, editors, dialogs and export.
- Direct numeric theta input and accessible name/value/range for the knob.
- Reduced-motion mode; no essential information conveyed only by animation.
- Contrast at least 4.5:1 for normal text and 3:1 for large text/meaningful graphics.
- Responsive split-pane behavior and user-adjustable editor/UI scale.
- Deterministic visual snapshots for empty, loading, success, warning, error and unknown states.

## 9. Release gates

A release candidate must include reproducible build instructions, locked dependencies, tests for each advertised stage, platform matrix, license inventory, SBOM, security review of the sandbox, benchmark metadata and export smoke tests. Windows x64/ARM64, macOS Apple Silicon/Intel and Linux Wayland/X11 remain separate targets until each is built and tested.

## 10. Implementation order

1. Rust workspace, profile schema, deterministic knob mapping and property tests.
2. Grammar/parser and diagnostics contract.
3. Type/effect checker with a deliberately small supported subset.
4. HIR/MIR and interpreter reference backend.
5. Native UI shell and accessible Massive Knob.
6. Cranelift JIT sandbox; optional Z3 and LLVM adapters.
7. LSP, stdlib, transpiler golden corpus and export packaging.
8. GPU optimization and cross-platform qualification based on measurements.
