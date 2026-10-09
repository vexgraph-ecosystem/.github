<p align="center">
  <a href="https://github.com/vex-graph"><img src="https://raw.githubusercontent.com/vex-graph/vex-graph/main/resources/vexgraph.png" alt="vexgraph" width="48%"></a>
  <img src="https://raw.githubusercontent.com/vex-graph/vex-graph/main/resources/ecosystem.png" alt="ecosystem" width="48%">
</p>

# vexgraph-ecosystem
My own ecosystem for relentless dogfooding

A vertically integrated, multi-repository systems engineering ecosystem built in
C23 with Rust-owned R2 storage and native C processing. Everything is a pointer.

> **Work in progress—not a finished product suite.** Repositories range from
> implemented slices to partial foundations and source-free blueprints. The R5
> apps in particular are unfinished: their descriptions are goals, not shipped
> IDE, DAW, spatial/drawing studio or game-engine capabilities. Consult the
> [readiness Gist](https://gist.github.com/vex-graph/6943f92acb931b25dad1073c46da6ce7) — see all [gists](https://gist.github.com/vex-graph).

I am a solo developer + I have an AI pair-programming pipeline that treats dense,
explicit, machine-readable architecture as a first-class artifact. No arrow
sugar. No hidden allocations on steady-state paths. No secrets in the arena.

## The Stack in one order: R1 to R5 system

The ecosystem follows a single runtime supervisor order. Lower R boots earlier,
is more stable, and tears down later.

| Runtime | Repo | Role                                                                    |
|---------|---|-------------------------------------------------------------------------|
| **R1**  | [`hotcwap`](https://github.com/vexgraph-ecosystem/hotcwap) | Host: process supervisor, Kernel, OS windows, dynamic hot-loader        |
| **R2**  | [`vexspoke`](https://github.com/vexgraph-ecosystem/vexspoke) | CPU computation, math, algorithms, synchronization and behavior |
| **R2**  | [`relational-engine`](https://github.com/vexgraph-ecosystem/relational-engine) | Memory/storage, stable row chunks, variable bindings and native C search |
| **R3**  | [`graphvex`](https://github.com/vexgraph-ecosystem/graphvex) | Driver: Vulkan/WGPU GPU pipelines, meshlets, fonts, SDF raster          |
| **R3**  | [`api-haven`](https://github.com/vexgraph-ecosystem/api-haven) | Driver: MCP/AI/DB/asset connector surface                               |
| **R3**  | [`language`](https://github.com/vexgraph-ecosystem/language) | Driver: LSP/grammar dylibs                                              |
| **R3**  | [`darkbase`](https://github.com/vexgraph-ecosystem/darkbase) | Driver: native vex database store                                       |
| **R3**  | [`samplerate`](https://github.com/vexgraph-ecosystem/samplerate) | Driver: native audio (CoreAudio/WASAPI/ALSA), DSP graph, render/export |
| **R4**  | [`darling-framework`](https://github.com/vexgraph-ecosystem/darling-framework) | Interfaces: widgets, layout, input/focus and host bridges; composition is R3 |
| **R4**  | [`sesh`](https://github.com/vexgraph-ecosystem/sesh) | Interfaces: session sync, VPS relay                                     |
| **R4**  | [`harness`](https://github.com/vexgraph-ecosystem/harness) | Interfaces: the user's own agent (projects/tools/R5 apps)                |
| **R5**  | [`semicolon`](https://github.com/vexgraph-ecosystem/semicolon) | Interactables: mini IDE (with big scope xd)                             |
| **R5**  | [`impedance`](https://github.com/vexgraph-ecosystem/impedance) | Interactables: bare-metal DAW (on the R3 samplerate engine)              |
| **R5**  | [`darling`](https://github.com/vexgraph-ecosystem/darling) | Interactables: spatial studio                                           |
| **R5**  | [`drawling`](https://github.com/vexgraph-ecosystem/drawling) | Interactables: drawing studio                                           |
| **R5**  | [`anti`](https://github.com/vexgraph-ecosystem/anti) | Interactables: 3D game engine                                           |

R2 migration is staged: existing Vexspoke memory/container ABI and its default
allocator remain until explicit migration and owner proof. No C/Rust atomic
layout equivalence or automatic schema migration is implied. R1 owns storage
lifetimes/residency; Graphvex owns GPU shaders/dispatch. R3 may borrow either
R2 public contract, but that permission is not an implemented dependency.

Standalone and in-tree runtime builds are architectural obligations, not blanket
readiness claims. Commit dependencies upstream-first (Relational Engine before
Vexspoke when it consumes that ABI, then R3 → R1 → R4 → R5); per-file commits may
depend on other records in the same verified work cycle.

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
