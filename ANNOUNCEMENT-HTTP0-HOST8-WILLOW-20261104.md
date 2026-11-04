# Project announcement — Host8 / USB storage, HTTP-0 physical compute and Willow-class benchmarks

**November 4, 2026 · Public source-and-results announcement · JesseBrown1980**

This repository connects three related, independently scoped pieces of the **classical CPU/storage research**: out-of-core Host8 room storage, the native HEB-C/HTTP-0 finite-state engine, and the Asolaria-versus-Willow-class integer benchmarks. The program implements reproducible computation on commodity CPU hardware and addressable storage; the available measurements concern the exact workloads listed below.

## 1. HTTP-0: from an addressable namespace to real computation

The earlier [HEB-C / HTTP-0 23-billion-address experiment (October 24, 2026)](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash/blob/main/HEBC_23B_VIRTUAL_PORTAL_REPORT.md) is the published launch/results record. It measured **1,990,656 distinct arithmetic address probes**, **28,236,255 probes/second**, **243 D3Q27 steps** on a synthetic **24³ × 27 = 373,248-channel** grid, exact conservation and reversal controls. The 23 billion positions were *virtual identifiers*: zero of those positions were instantiated as separate network services, and the old browser benchmark executed zero actual HTTP connections.

The more recent [3¹⁶ Clay/Taylor bridge](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash/blob/main/docs/HTTP0-CLAY-3POWER16-BRIDGE.md) and [Yang–Mills certificate bridge](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash/blob/main/docs/HTTP0-YANG-MILLS-3POWER16.md) add a **43,046,721-position** sparse ternary namespace with **732 occupied evidence/observation addresses**: 729 Clay/Taylor–Green register observations and three Yang–Mills source receipts. Lookups verify pinned source bytes; they do not recompute the complete Yang–Mills Hamiltonian.

**The computational upgrade is now real:** [HTTP-0 PR #3, merged](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash/pull/3), adds a native Rust 1.81 D3Q27 CPU engine for the following lattice sizes.

| Grid | Mutated physical ternary channels | Two in-memory trit buffers | Measured 3-step forward time |
|---|---:|---:|---:|
| 24³ × 27 | 373,248 | 746,496 bytes | 0.016446135 s (new) / 0.014188226 s (original) |
| 48³ × 27 | 2,985,984 | 5,971,968 bytes | 0.128052008 s |
| **96³ × 27** | **23,887,872** | **47,775,744 bytes** | **1.025157327 s** |

The [source-backed measurement HBP](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash/blob/main/engine96/MEASURED-20261104.hbp) records conservation of integer mass, momentum and energy, exact three-step reversal and matching 24³ legacy output. Separate 96³ hosted runs measured approximately 0.889–1.025 seconds for three steps. The new general-purpose 24³ path was slightly slower than the original at 24³; **no general speedup over an alternative solver or GPU has been established**. The full 192-step externally driven Taylor–Green cutoff and its preserved **C1 PASS / A1 FAIL** are [a distinct experiment](https://github.com/JesseBrown1980/Taylor_green_regularity-resolved-and-solved/tree/main/results/2026-10-30-cutoff).

Reproduce physical computation in the [HTTP-0 source repository](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash):

```bash
cargo +1.81.0 run --release --locked --offline -- --bench-engine 96 3
```

## 2. How USB/SSD storage fits

Host8 uses **8-byte packed rooms with 27 ternary positions** and fixed-address sector windows. The documented 300 GB sector-store geometry provides up to **37.5 billion addressable rooms**. CPU workers can read bounded windows instead of allocating an equally large GPU VRAM buffer. This is useful for **discrete integer algorithms that have been implemented for streaming or indexed access**. It is an input/data-storage architecture; reading a sector or calculating a room address does not itself perform a Hamiltonian evolution or replace GPU arithmetic for unrelated algorithms.

Sources: [Host8 native implementation and times](https://github.com/JesseBrown1980/finite-reversible-ternary-physics/blob/main/HOST8_LOCAL_PHYSICS_BENCHMARK_TIMINGS.md), [Rust room/audit tools](https://github.com/JesseBrown1980/Clasy-repo-x-3-/blob/main/src/bin/audit_rooms.rs), [HEB-C physical-source cross-check](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash/blob/main/CROSS_VALIDATION_HOST8_HEBC_REPORT.md), and [Willow project 100 GB mapped-sector study](https://github.com/JesseBrown1980/Asolaria-VS-GOOGLE-Willow-chip/blob/main/WILLOW-VS-ASOLARIA-REPORT.md). An actual cold drive, an OS-cached mapped file and an arithmetic-only generated address have different performance characteristics.

## 3. Asolaria-versus-Willow-class results (October 22, 2026)

The [Asolaria/Willow classical benchmark](https://github.com/JesseBrown1980/Asolaria-vs-Williow-chip-Results) uses exact **27-lane finite-field Number-Theoretic Transforms**, coupled into a **108-lane** 40-layer workload. Its [ten-run SHA-linked result source](https://github.com/JesseBrown1980/Asolaria-vs-Williow-chip-Results/blob/main/receipts/WILLOW-10RUNS-MAXTRITS-20261022.hbp) records:

| Measurement in the Asolaria test suite | Recorded result |
|---|---|
| 108-lane depth-40 classical transform workload | **80,000** circuits across ten runs |
| Average simulated-workload latency | **290 microseconds per circuit** (minimum 270, maximum 312) |
| Finite-field Parseval and round-trip checks | **12,800,000** each, all marked EXACT |
| Classical stabilizer-decoding test | **70,000** registered rounds at code distances 3–27, 7–8 µs/round in this receipt |
| Procedural coordinate-plane sweep | **100 million sampled addresses** across a nominal 12.5-billion-address domain |

The separate [five-tier mapped-storage and circuit report](https://github.com/JesseBrown1980/Asolaria-VS-GOOGLE-Willow-chip/blob/main/WILLOW-VS-ASOLARIA-REPORT.md) records **100 GB / 125 mapped sectors**, an observed **743 million room reads/second** for a sampled mapped-memory sweep and **about 838 microseconds** for its mapped-sector 108-lane depth-40 workload. These are different benchmark configurations from the ten-run 290 µs result and must not be combined as one timing.

**Comparison boundary:** These are **classical finite-field and coordinate-bijection workloads**. Their 108 integer lanes are not 105 quantum-mechanical qubits, and the NTT workload is not a demonstration of faithfully sampling Google's 105-physical-qubit random-circuit output distribution, implementing Willow's physical error-suppression experiment or outperforming Willow on an identical task. The storage/coordinate count is not a fully simulated quantum state vector.

The executable comparison and receipts are linked through [Willow results and limitations](https://github.com/JesseBrown1980/Asolaria-vs-Williow-chip-Results/blob/main/RESULTS.md), [5-tier Willow-class report](https://github.com/JesseBrown1980/Asolaria-VS-GOOGLE-Willow-chip/blob/main/WILLOW-VS-ASOLARIA-REPORT.md) and [Asolaria Willow source benchmark](https://github.com/JesseBrown1980/Asolaria-VS-GOOGLE-Willow-chip/blob/main/shared-runtime/examples/willow_room_bench.rs).

## 4. What the announcement establishes

**Public, reproducible classical software milestones:** a 23-billion-ID arithmetic address test, an authenticated sparse 3¹⁶ evidence catalog, a physically computed 96³ D3Q27 lattice, indexed Host8/USB/SSD research and separately documented finite-field Willow-class experiments. The underlying measurements, commands and original records are linked above.

**Outstanding work:** a controlled external-GPU comparison on identical tasks; end-to-end full-storage throughput including cold I/O; the complete driven 96³ Taylor–Green replay; any equivalence to a physical quantum processor; and any continuum Yang–Mills mass-gap claim. Future results should include exact source commits, state hashes, time measurements, resource usage, and preserved FAIL/OPEN outcomes.

This document is the **November 4, 2026 source-linked project announcement**, adding the recent HTTP-0 physical-computation upgrade to the earlier October 24 HTTP-0 announcement record and October 22 Willow-class benchmark reports.
