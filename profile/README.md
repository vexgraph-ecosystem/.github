<p align="center">
  <a href="https://github.com/vex-graph"><img src="https://raw.githubusercontent.com/vex-graph/vex-graph/main/resources/vexgraph.png" alt="vexgraph" width="48%"></a>
  <img src="https://raw.githubusercontent.com/vex-graph/vex-graph/main/resources/ecosystem.png" alt="ecosystem" width="48%">
</p>

# vexgraph-ecosystem
My own ecosystem for relentless dogfooding

A vertically integrated, multi-repository systems engineering ecosystem built in
C23 with Rust-owned R1 storage and native C processing. Everything is a pointer.

> **Work in progress—not a finished product suite.** Repositories range from
> implemented slices to partial foundations and source-free blueprints. The R5
> apps in particular are unfinished: their descriptions are goals, not shipped
> IDE, DAW, spatial/drawing studio or game-engine capabilities. Consult the
> [readiness Gist](https://gist.github.com/vex-graph/6943f92acb931b25dad1073c46da6ce7) — see all [gists](https://gist.github.com/vex-graph).

I am a solo developer + I have an AI pair-programming pipeline that treats dense,
explicit, machine-readable architecture as a first-class artifact. No arrow
sugar. No hidden allocations on steady-state paths. No secrets in the arena.

## Current State

**Implemented:** the repository set, the `b`-driven build entry, the R0–R6
repositories at mixed readiness, the shared [`tests`](https://github.com/vexgraph-ecosystem/tests)
suite, and the constitution plus its Gists. **Proven:** macOS builds and the
scoped test suites recorded in the workspace test checklist; see the readiness
Gist. **Not finished:** the R5 applications and R6 superapps are shells,
scaffolds or blueprints, and several R3/R4 repositories are blueprints.

## Scope and Limitations

**Scope:** a vertically integrated C23/Rust ecosystem — R0 host, R1 storage and
module reload, R2 computation, R3 drivers, R4 interfaces, R5 interactables, R6
superapps — plus the personal `b` and `func` tools. **Deliberately not covered:**
no monorepo (each repository is independent) and no platform promise beyond the
stated floor. **Known limits and gaps:** Windows/Linux runtime proof, GPU/audio
runtime proof, and application completion are outstanding; nothing here is a
finished product suite.

## The Stack in one order: R0 to R6 system

The ecosystem follows a single runtime supervisor order. R0 boots first; lower R
is more stable and tears down later.

| Runtime | Repo | Role |

|---------|---|-------------------------------------------------------------------------|
| **R0**  | [`lifetime`](https://github.com/vexgraph-ecosystem/lifetime) | Kernel host: process/application lifecycle, lifetimes, native OS windowing, capability gating and memory substrate attestation |
| **R1**  | [`relational-engine`](https://github.com/vexgraph-ecosystem/relational-engine) | Memory/storage, stable row chunks, variable bindings, cache and native C search |
| **R1**  | [`hotcwap`](https://github.com/vexgraph-ecosystem/hotcwap) | Dynamic module reloading and ABI airlock — optional per app |
| **R2**  | [`vexspoke`](https://github.com/vexgraph-ecosystem/vexspoke) | CPU computation, math, algorithms, synchronization, behavior and network protocols |
| **R3**  | [`graphvex`](https://github.com/vexgraph-ecosystem/graphvex) | Driver: Vulkan/WGPU GPU pipelines, meshlets, fonts, SDF raster          |
| **R3**  | [`api-haven`](https://github.com/vexgraph-ecosystem/api-haven) | Driver: MCP/AI/DB/asset connector surface                               |
| **R3**  | [`language`](https://github.com/vexgraph-ecosystem/language) | Driver: LSP/grammar dylibs                                              |
| **R3**  | [`darkbase-engine`](https://github.com/vexgraph-ecosystem/darkbase-engine) | Driver: native vex database store                            |
| **R3**  | [`samplerate`](https://github.com/vexgraph-ecosystem/samplerate) | Driver: native audio (CoreAudio/WASAPI/ALSA), DSP graph, render/export |
| **R3**  | [`determinant`](https://github.com/vexgraph-ecosystem/determinant) | Driver: terminal rendering, widgets, CLI parsing and caller-fed input |
| **R4**  | [`darling-framework`](https://github.com/vexgraph-ecosystem/darling-framework) | Interfaces: widgets, layout, input/focus and host bridges; composition is R3 |
| **R4**  | [`sesh`](https://github.com/vexgraph-ecosystem/sesh) | Interfaces: session sync, VPS relay                                     |
| **R4**  | [`harness`](https://github.com/vexgraph-ecosystem/harness) | Interfaces: the user's own agent loop (projects/tools/R5 apps)          |
| **R4**  | [`darkbase-headless`](https://github.com/vexgraph-ecosystem/darkbase-headless) | Interfaces: service boundary over the R3 store               |
| **R5**  | [`impedance`](https://github.com/vexgraph-ecosystem/impedance) | Interactables: bare-metal DAW (on the R3 samplerate engine)              |
| **R5**  | [`darling`](https://github.com/vexgraph-ecosystem/darling) | Interactables: spatial studio                                           |
| **R5**  | [`drawling`](https://github.com/vexgraph-ecosystem/drawling) | Interactables: drawing studio                                           |
| **R6**  | [`semicolon`](https://github.com/vexgraph-ecosystem/semicolon) | Superapp: IDE workflows, Language/b tooling and future standalone Primeagen integration |
| **R6**  | [`anti`](https://github.com/vexgraph-ecosystem/anti) | Superapp: IDE, DAW, drawing and creative/game workflow composition |

R2 migration is staged: the existing Vexspoke memory/container ABI and its
default allocator remain until explicit migration and owner proof. No C/Rust
atomic layout equivalence or automatic schema migration is implied. R0 owns
residency and hardware ground truth; R1 owns storage and its lifetimes;
Graphvex owns GPU shaders/dispatch. R3 may borrow either the R1 storage or the
R2 computation public contract, but that permission is not an implemented
dependency.

Standalone and in-tree runtime builds are architectural obligations, not blanket
readiness claims. Commit dependencies upstream-first (Relational Engine before
Vexspoke when it consumes that ABI, then R0 → R1 → R2 → R3 → R4 → R5 → R6);
per-file commits may depend on other records in the same verified work cycle.

## Personal parts: standalone first, a `+1` dependency second

Some parts deliberately live in my personal accounts instead of this org. They
carry none of the ecosystem's baggage: no R-tier boot obligation, no in-tree
build requirement, no ecosystem-wide contract to keep in step. That is the point
— they stand alone, ship on their own schedule, and stay useful to someone who
never clones the ecosystem.

| Repo | Account | Stands alone as | Optional `+1` for |
|---|---|---|---|
| [`b`](https://github.com/vex-graph/b) | personal | the build/run CLI (`run`, `build`, `export`) | this workspace's target graph and any standalone project |
| [`func`](https://github.com/vex-graph/func) | personal | a compile-time opcode orchestrator | ecosystem libraries that want it, and nothing else |
| [`primeagen`](https://github.com/vex-graph/primeagen) | personal | an R5-style workflow tool | semicolon, as a future integration |
| [`darkbase`](https://github.com/vex-graph/darkbase) | personal | a host over the R3 darkbase store | apps that want a darkbase consumer |

The dependency rule is one-directional and never a requirement: a personal part
must build and run with no ecosystem checkout, the ecosystem may reference one as
an optional dependency, and an R-tier capability that leans on one is itself
optional and must state what it does without it. Ownership is not optionality:
`hotcwap`, `api-haven` and `harness` are optional per app but remain
ecosystem-owned repositories, and they stay listed in the stack above.

## The Law

Architecture is governed by a living constitution through
[preferences.md](https://gist.github.com/vex-graph/4132a6c45cb6d3797c3e8eff2e94035a).
It has Tier 1 memory invariants, Tier 2 object model, and Tier 3 syntactic determinism.

## Notable non-negotiables:

- `(*ptr).field` — never `->`; every dereference is explicit.
- One class per file. One problem in one file stays in one file.
- Dest-last outputs. Two-layer access cap. Symmetric getters/setters.
- Zero steady-state allocation. Bounded waits on every joined thread.
- Teardown runs top-down; `Memory_freeAll` is always last.

## Reading a repository

This profile describes the **intended** ownership of an unfinished ecosystem.
Read each repository's own `## Current State` and `## Scope and Limitations`
before treating any capability as shipped, and consult the readiness Gist and
the workspace test checklist for the evidence of record.
