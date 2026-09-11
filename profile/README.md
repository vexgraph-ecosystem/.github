# vexgraph-ecosystem

A sovereign, vertically integrated C23 software suite built on pure pointers,
zero steady-state allocation, and hardware-accelerated Vulkan/WGPU graphics.

Everything is a pointer.

---

## The R1-R5 Runtime Architecture

The ecosystem follows a strict, single vertical order of supervision: lower
tiers boot earlier, maintain higher memory stability, and tear down last.

```text
R1 Host        hotcwap       — process supervisor, Kernel, OS windows,
                               dynamic hot-loader, lifecycle
R2 Behavior    vexspoke      — relational memory arena, BitPool, Variable,
                               types, dest-last math, sync
R3 Drivers     graphvex      — GPU/WGPU driver, fonts, SDF raster, meshlets
               api-haven     — MCP / AI / DB / asset connector surface
               language      — grammar dylibs and LSP engines
               darkbase      — native vex database store
R4 Interfaces  darling-framework — retained UI toolkit, 9-grid layout,
                                   multi-layer compositor
               sesh          — session sync, VPS relay, bug ingestion
R5 Interactables
               semicolon     — mini IDE
               samplerate    — bare-metal DAW
               darling       — spatial studio (darling-editor)
               drawling      — drawing studio
               anti          — 3D game engine
```

Every repository stays buildable standalone and in-tree. Cross-cutting changes
commit upstream-first (R2 -> R3 -> R1 -> R4 -> R5) so every commit is atomic
and bisectable.

---

## Core Invariants

1. **Zero steady-state allocation.** The memory arena carves once from the OS;
   pools, rings, and tables recycle in-place. Zero `malloc` on the 60/120fps
   hot path.
2. **Embrace the pointer.** Field access is always `(*ptr).field`, never `->`.
   Explicit dereferencing makes the hardware cost visible.
3. **No pointer chasing.** Hardware memory access is one level + offset. Access
   is capped at two layers; anything deeper hoists into a local register.
4. **One class per file (the Java Law).** One public class struct per `.h`/`.c`
   pair. One problem in one file stays in one file.
5. **Dest-last. Symmetric getters/setters. Bounded waits on every joined
   thread. Teardown runs top-down; `Memory_freeAll` dead last.**

---

## Repositories

| Repository | Tier | Description |
|:---|:---:|:---|
| [`hotcwap`](https://github.com/vexgraph-ecosystem/hotcwap) | **R1 Host** | Kernel host supervisor, multi-app registry, native windowing, hot-loader |
| [`vexspoke`](https://github.com/vexgraph-ecosystem/vexspoke) | **R2 Behavior** | Pure relational leaf: MemoryArena, BitPool, Variable, math, system probes |
| [`graphvex`](https://github.com/vexgraph-ecosystem/graphvex) | **R3 Driver** | GPU/WGPU compute, meshlets, SDF font/icon atlas, shaders |
| [`api-haven`](https://github.com/vexgraph-ecosystem/api-haven) | **R3 Driver** | Connectors: AI/DB catalogs, MCP server, blessed asset broker |
| [`language`](https://github.com/vexgraph-ecosystem/language) | **R3 Driver** | Relational AST engine & hot-loadable grammar modules |
| [`darkbase`](https://github.com/vexgraph-ecosystem/darkbase) | **R3 Driver** | Database switchboard & native vex relational store |
| [`darling-framework`](https://github.com/vexgraph-ecosystem/darling-framework) | **R4 Interface** | Pure UI toolkit: 9-grid layout, widget library, multi-layer compositor |
| [`sesh`](https://github.com/vexgraph-ecosystem/sesh) | **R4 Interface** | Session sync, live cursor pairing, VPS relay, in-engine bug ingestion |
| [`darling`](https://github.com/vexgraph-ecosystem/darling) | **R5 Interactable** | Spatial studio (darling-editor): Figma + Miro inspired whiteboard |
| [`semicolon`](https://github.com/vexgraph-ecosystem/semicolon) | **R5 Interactable** | Stripped mini-IDE, shell-out toolchains, AST navigation |
| [`drawling`](https://github.com/vexgraph-ecosystem/drawling) | **R5 Interactable** | Drawing layers, stroke ring undo, animation timelines |
| [`samplerate`](https://github.com/vexgraph-ecosystem/samplerate) | **R5 Interactable** | Bare-metal DAW, realtime mixer core, spatial binaural HRTF |
| [`anti`](https://github.com/vexgraph-ecosystem/anti) | **R5 Interactable** | 3D game engine, bindless geometry, reversible physics |

---

## The AI-First Architecture Manifesto

This ecosystem is an intentional manifesto of **AI-Human Pair Systems
Programming**.

The dense, explicit boilerplate across the codebase is not a misunderstanding
of idiomatic C — it is a machine-readable safety scaffold. The human architect
directs high-level invariants, algorithms, and concurrency semantics, while the
AI agent reliably writes, audits, refactors, and verifies the explicit
getters, setters, overviews, and constructor dispatches.

> [!WARNING]
> **SANITY NOTICE FOR EXTERNAL CONTRIBUTORS**
> The upstream codebase is exclusively maintained by its author in tandem with
> an AI pair. We do not accept pull requests attempting to re-introduce `->`,
> collapse multiple classes into single files, eliminate explicit
> getters/setters, or "modernize" the code against our architectural doctrine.

The constitution everything follows:
[`preferences.md`](https://github.com/vexgraph-ecosystem/vexspoke/blob/main/preferences.md)