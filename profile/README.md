# vexgraph-ecosystem
My own ecosystem for relentless dogfooding

A vertically integrated, multi-repository systems engineering ecosystem built in
pure C23. Everything is a pointer. and it will be, conceptually and implementedly.

I am a solo developer + I have an AI pair-programming pipeline that treats dense,
explicit, machine-readable architecture as a first-class artifact. No arrow
sugar. No hidden allocations on steady-state paths. No secrets in the arena.

## The Stack in one order: R1 to R5 system

The ecosystem follows a single runtime supervisor order. Lower R boots earlier,
is more stable, and tears down later.

| Runtime | Repo | Role                                                                    |
|---------|---|-------------------------------------------------------------------------|
| **R1**  | [`hotcwap`](https://github.com/vexgraph-ecosystem/hotcwap) | Host: process supervisor, Kernel, OS windows, dynamic hot-loader        |
| **R2**  | [`vexspoke`](https://github.com/vexgraph-ecosystem/vexspoke) | Behavior: relational memory arena, BitPool, types, dest-last math, sync |
| **R3**  | [`graphvex`](https://github.com/vexgraph-ecosystem/graphvex) | Driver: Vulkan/WGPU GPU pipelines, meshlets, fonts, SDF raster          |
| **R3**  | [`api-haven`](https://github.com/vexgraph-ecosystem/api-haven) | Driver: MCP/AI/DB/asset connector surface                               |
| **R3**  | [`language`](https://github.com/vexgraph-ecosystem/language) | Driver: LSP/grammar dylibs                                              |
| **R3**  | [`darkbase`](https://github.com/vexgraph-ecosystem/darkbase) | Driver: native vex database store                                       |
| **R4**  | [`darling-framework`](https://github.com/vexgraph-ecosystem/darling-framework) | Interfaces: retained UI toolkit, scene graphs, compositor               |
| **R4**  | [`sesh`](https://github.com/vexgraph-ecosystem/sesh) | Interfaces: session sync, VPS relay                                     |
| **R5**  | [`semicolon`](https://github.com/vexgraph-ecosystem/semicolon) | Interactables: mini IDE (with big scope xd)                             |
| **R5**  | [`samplerate`](https://github.com/vexgraph-ecosystem/samplerate) | Interactables: bare-metal DAW                                           |
| **R5**  | [`darling`](https://github.com/vexgraph-ecosystem/darling) | Interactables: spatial studio                                           |
| **R5**  | [`drawling`](https://github.com/vexgraph-ecosystem/drawling) | Interactables: drawing studio                                           |
| **R5**  | [`anti`](https://github.com/vexgraph-ecosystem/anti) | Interactables: 3D game engine                                           |

Every repository stays buildable standalone and in-tree. Cross-cutting changes
commit upstream-first (R2 → R3 → R1 → R4 → R5) so every commit is atomic and
bisectable.

## The Law

Architecture is governed by a living constitution:
<p>
[`preferences.md`](https://github.com/vexgraph-ecosystem/vexspoke/blob/main/preferences.md)
</p>
It has Tier 1 memory invariants, <p>Tier 2 object model, <p> and Tier 3 syntactic determinism.

## Notable non-negotiables:

- `(*ptr).field` — never `->`; every dereference is explicit.
- One class per file. One problem in one file stays in one file.
- Dest-last outputs. Two-layer access cap. Symmetric getters/setters.
- Zero steady-state allocation. Bounded waits on every joined thread.
- Teardown runs top-down; `Memory_freeAll` is always last.