# Hard Drive and USB Storage as Compute Substrate

Out-of-core memory addressing (Host8 / SG-RAM), native HEB-C/HTTP-0 D3Q27 CPU computation, and classical integer/ternary benchmarks across the Jesse Daniel Brown research repositories.

---

## Latest announcement and connected results — November 4, 2026

**[Read the public project announcement with source links, measured results and open controls](ANNOUNCEMENT-HTTP0-HOST8-WILLOW-20261104.md).**

**[Reverse-history repository map: QNN → Google circuits → HTTP-0 → Host8 → YM4 → finite Yang–Mills → Clay → Willow](ECOSYSTEM-RESEARCH-MAP-20261104.md)**. Includes 17 verified source repositories, their roles, results and open gates.

**New official Google-circuit comparison (November 4):** [QNN PR #6](https://github.com/JesseBrown1980/GGUF-files-operating-as-trained-quantum-neural-network-models/pull/6) reproduced **Google's full published 24-qubit 1,257-gate circuit** and directly compared 64 complex amplitudes against Google's pinned upstream `qsim_amplitudes`: **128/128 real/imaginary components within 10⁻⁶**, largest difference **1.667 × 10⁻⁹**, and **128/128 components rejected** when the √Y gate sign was deliberately changed. [Frozen run/receipt](https://github.com/JesseBrown1980/GGUF-files-operating-as-trained-quantum-neural-network-models/blob/main/docs/GOOGLE-QSIM-OFFICIAL-REFERENCE-20261104.hbp) and [hosted source-matched result](https://github.com/JesseBrown1980/GGUF-files-operating-as-trained-quantum-neural-network-models/actions/runs/41926857572). The [HTTP-0 23,887,872-qutrit integration](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash/pull/5) adds a separately measured large-register computation.


- **[HTTP-0 actual physical engine](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash/pull/3):** Rust 1.81 now advances **96³ × 27 = 23,887,872 real D3Q27 trit channels**, with exact conservation and three-step reversal checks. [Measured 24³/48³/96³ timings and state hashes](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash/blob/main/engine96/MEASURED-20261104.hbp).
- **[HTTP-0 original public results/announcement record (October 24)](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash/blob/main/HEBC_23B_VIRTUAL_PORTAL_REPORT.md):** 23 billion **virtual identifiers** with 1,990,656 actual probes. The [new 3¹⁶ certificate catalog](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash/blob/main/docs/HTTP0-YANG-MILLS-3POWER16.md) has **43,046,721 virtual slots** and **732 populated observations/receipts**; these addresses are distinct from physical computation.
- **[Asolaria-versus-Willow-class results](https://github.com/JesseBrown1980/Asolaria-vs-Williow-chip-Results/blob/main/RESULTS.md):** [the ten-run source receipt](https://github.com/JesseBrown1980/Asolaria-vs-Williow-chip-Results/blob/main/receipts/WILLOW-10RUNS-MAXTRITS-20261022.hbp) records **80,000 classical 108-lane circuits, a 290 µs mean, 12.8 million exact finite-field transform checks and 70,000 test decoding rounds**. The separate [five-tier mapped 100 GB store and Willow-class benchmark](https://github.com/JesseBrown1980/Asolaria-VS-GOOGLE-Willow-chip/blob/main/WILLOW-VS-ASOLARIA-REPORT.md) includes measured memory-access and circuit times.

## 1. Architectural Overview: Secondary Storage as Addressed Memory

Traditional deep learning, simulation, and scientific compute frameworks require tens to hundreds of gigabytes of expensive, dedicated GPU VRAM (e.g. H100/A100 clusters) and large system RAM pools. They rely heavily on floating-point general matrix multiplies (GEMM), incurring high memory bandwidth costs, cloud expenses, and PCIe bus transfer latency.

This repository documents the **Host8 / SG-RAM / Out-of-Core Architecture** established across Jesse Daniel Brown's codebase:
1. **Secondary Storage as Linear Memory**: High-capacity secondary storage (such as a 300 GB NVMe/SSD drive, local disk, or USB storage dock) is partitioned into fixed-size binary sector files and addressed directly via $O(1)$ linear byte offsets.
2. **CPU Integer Register Streaming**: Instead of loading hundreds of gigabytes into RAM or offloading to a GPU, lightweight CPU worker threads stream sequential windows through bounded, cache-friendly buffers (e.g. 4 MiB in CPU L3 cache).
3. **No GPU Required (`gpu_calls = 0`)**: All computational dynamics are formulated as exact integer permutations, discrete balanced-ternary gates, involutive collision operators ($U = U^{-1}$), or finite-field transforms. Standard CPU ALUs evaluate these discrete transitions faster than PCIe transfer overhead to an external GPU.

---

## 2. Core Repository Implementations

The architecture is documented across four compute/storage repositories, with a linked fifth repository for Willow-class benchmark evidence:

### A. [`Clasy-repo-x-3-`](https://github.com/JesseBrown1980/Clasy-repo-x-3-) *(Rust 1.81 Native Streaming Engine)*
- **Key Modules**:
  - `src/bin/sweep_rooms.rs`: Multithreaded direct disk streamer reading from `D:/ASOLARIA-HOST8-ROOMS-300G`.
  - `src/bin/audit_rooms.rs`: Fail-closed 81/243-room read-only Host8 evaluator enforcing `gpu_calls=0`, `mcp_calls=0`, `provider_calls=0`, `float_used=0`.
  - `src/host8_audit.rs`: Host8 plane codec and canonical address bounds check.
- **Execution Mechanism**:
  - Streams 24-byte ensembles (3 rooms $\times$ 8 bytes = 81 trits) from disk into 4 MiB thread buffers (`BufReader::with_capacity(4 * 1024 * 1024, file)`).
  - Evaluates exact 81-point spherical NTT transforms and all-time polynomial invariants directly in CPU registers without GPU memory.

### B. [`finite-reversible-ternary-physics`](https://github.com/JesseBrown1980/finite-reversible-ternary-physics) *(Native C++ Host8 Substrate)*
- **Key Modules**:
  - `HOST8_LOCAL_PHYSICS_BENCHMARK_TIMINGS.md`: Timing benchmarks across 375 physical sector files.
  - `asolaria_equilibrium_suite.cpp`: Core D3Q27 lattice gas simulator executing directly on disk sectors.
  - `run_physical_window_243.cpp`: Physical window runner over the 300 GB dataset.
- **Measured CPU Throughput**:
  - Processes 288 mass- and momentum-conserving collision gates at **1,620,190 rooms/second** (>43.7 million trits/second) on a commodity AMD Ryzen CPU with 0 GPU utilization.
  - Evaluates 48 forward ticks + 16 forward/backward Loschmidt reversibility cycles with $0$ bit mismatches across 139.9 million trits in 263.2 seconds (~4.4 minutes).

### C. [`CORRECTION-TO-ASOLARIA-AND-FAULT-TO-OPEN-AI-NAVIER-STOKES-SOLUTIONS-SOLVED`](https://github.com/JesseBrown1980/CORRECTION-TO-ASOLARIA-AND-FAULT-TO-OPEN-AI-NAVIER-STOKES-SOLUTIONS-SOLVED) *(Finiteness Principle & Hardware Substrate)*
- **Key Modules**:
  - `PROOF.md` (§4 & §5): Physical hardware instantiation in the 300 GB Host8 store.
  - `README.md`: Contrast between discrete physical home-computer execution and continuum GPU cluster simulations.
- **Physical Instantiation**:
  - Grounded across the **300 GB Host8 store** (`D:\ASOLARIA-HOST8-ROOMS-300G`, 37.5 billion rooms) and the **100 GB Falcon phone dock** (`D:\ASOLARIA-PHONE-FALCON-DOCK`), executing with integer-only precision and zero floating-point roundoff.

### D. [`qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash`](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash) *(HTTP-0 source catalog, native CPU engine and local portal)*
- **Key Modules**:
  - `CROSS_VALIDATION_HOST8_HEBC_REPORT.md`: Physical 300 GB block execution and cross-executor verification.
  - `CANONICAL_RUST_HEBC_REPORT.md` & `REPRODUCE_NATIVE_RUST_181.md`: Headless, browser-independent execution with zero external cloud dependencies.
- **Virtual Memory Coprimality**:
  - Maps 23 billion logical process instances in $O(1)$ space using coprime hashing:
    $$\text{virtual\_id} = (\text{ordinal} \times 1,000,003) \pmod{23,000,000,000}$$
  - Unoccupied instances require **0 in-memory allocations**, allowing a machine with standard RAM and no GPU to achieve 28.2 million address probes/second.
- **New physical update engine:** [`src/scale96.rs`](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash/blob/main/src/scale96.rs) computes the actual 24³, 48³ and **96³** D3Q27 states. At 96³, two 1-byte-per-trit state buffers total **47,775,744 bytes**. The [3-step CI receipt](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash/blob/main/engine96/MEASURED-20261104.hbp) records **1.025157327 seconds**, conserved integer invariants, full reversal and 24³ old-engine byte equality. The original engine at 24³ was faster in this controlled pair.
- **Evidence service:** [Clay/Taylor 729-register bridge](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash/blob/main/docs/HTTP0-CLAY-3POWER16-BRIDGE.md) and [Yang–Mills three-receipt bridge](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash/blob/main/docs/HTTP0-YANG-MILLS-3POWER16.md) share a sparse 3¹⁶ catalog with **732 occupied addresses**. Read-only source-integrity checks verify evidence without rerunning the Yang–Mills Hamiltonian.

### E. [`Asolaria-vs-Williow-chip-Results`](https://github.com/JesseBrown1980/Asolaria-vs-Williow-chip-Results) *(Classical integer benchmark and sealed receipts)*
- **Result sources:** [`RESULTS.md`](https://github.com/JesseBrown1980/Asolaria-vs-Williow-chip-Results/blob/main/RESULTS.md), [ten-run HBP](https://github.com/JesseBrown1980/Asolaria-vs-Williow-chip-Results/blob/main/receipts/WILLOW-10RUNS-MAXTRITS-20261022.hbp), and the [original five-tier Willow-class study](https://github.com/JesseBrown1980/Asolaria-VS-GOOGLE-Willow-chip/blob/main/WILLOW-VS-ASOLARIA-REPORT.md).
- **Registered classical workload:** 80,000 depth-40 transformations across 108 NTT lanes with **290 µs mean**, **12,800,000 exact Parseval/round-trip checks** and 70,000 synthetic syndrome test rounds. These timings characterize integer/ternary test code on a CPU; the reports do not establish same-task quantum-computer performance.

---

## 3. Physical Storage Geometry & Addressing

| Metric | Specification |
|---|---|
| **Storage Medium** | Secondary SSD / NVMe / USB storage volume (`D:\ASOLARIA-HOST8-ROOMS-300G`) |
| **Physical Capacity** | 300,000,000,000 bytes (300 GB) |
| **File Partitioning** | 375 binary sector files (`sector-000.rooms` to `sector-374.rooms`), exactly 800 MB each |
| **Room Dimensions** | 1 process room = 8 bytes (64-bit integer word `u64`) |
| **Total Process Rooms** | $375 \times 100,000,000 = \mathbf{37,500,000,000}$ rooms |
| **State Density** | 27 balanced trits ($\{-1, 0, +1\}$) packed per 64-bit room ($3^{27} \approx 7.62 \times 10^{12}$ states) |
| **Addressing Method** | Direct linear file seek: $\text{byte\_offset} = \text{room\_offset} \times 8$ |

```text
Host8 300 GB Disk Geometry:
  [sector-000.rooms] -> 100,000,000 rooms (800 MB)
  [sector-001.rooms] -> 100,000,000 rooms (800 MB)
  ...
  [sector-374.rooms] -> 100,000,000 rooms (800 MB)
  Total: 375 sectors = 37.5 Billion Rooms = 1.0125 Trillion Trits
```

---

## 4. Why CPU Streaming Replaces GPU VRAM

```text
 Traditional Cloud GPU Pipeline          Jesse Daniel Brown Host8 / SG-RAM Pipeline
 ─────────────────────────────          ──────────────────────────────────────────
 • Allocate 80 GB+ GPU VRAM             • 300 GB NVMe/SSD/USB Volume (37.5B Rooms)
 • Floats (f32/f64) with roundoff       • Exact Integer/Ternary (27 Trits per 8-Byte Room)
 • Cloud / CUDA driver dependency       • Direct O(1) Seek: byte_offset = room_idx * 8
 • High PCIe bus transfer latency       • Bounded 4 MiB buffer in CPU L3 cache
 • Millions of dollars in GPUs          • Involutive integer gates (U = U⁻¹) executed in ALU
                                        • gpu_calls = 0, float_used = 0, Cost = $0
```

1. **Elimination of Floating-Point GEMM**:
   Because the state space is discrete and operations are unitary/involutive permutations ($U = U^{-1}$), execution requires only bitwise shifts, masks, and integer additions. CPU execution units process these operations in single-cycle instructions without numerical drift.
2. **Cache-Friendly Streaming**:
   Instead of loading the entire 300 GB space into memory, worker threads read fixed chunks (e.g. 110,592 bytes = 13,824 rooms) into an L3-cache-friendly 4 MiB buffer. The computation completes while the data is in cache, streaming forward without memory thrashing.
3. **Zero Bus Latency**:
   PCIe transfer of hundreds of gigabytes between host RAM and GPU VRAM represents a major bottleneck in standard compute pipelines. Streaming directly from disk into CPU cache avoids GPU host-to-device transfers entirely.

---

## 5. HTTP-0 Portal Architecture & Zero-Cost Infrastructure

The companion HTTP-0 portal architecture introduced in `qoled-internet-HEB-C-revisted...` demonstrates how local visualization and inspection run at **$0 cost** on consumer hardware:

1. **Zero-JavaScript HTTP-0 Portal**:
   - Loopback TCP server (`127.0.0.1:5088`) written in native Rust (`std::net::TcpListener`).
   - Pure semantic HTML5 and CSS with **strictly zero JavaScript** (`<script>` tags forbidden).
   - Generates and streams standard uncompressed 24-bit BMP frames ($288 \times 288$ pixels) directly from discrete integer lattice trits using native HTML `<img>` tag refreshing.
2. **Native Cryptographic Fabric (HBI / HBP / SHA / ANCHOR)**:
   - Eliminates JSON serialization overhead (`json=0`).
   - **HBP (Hash-Based Provenance)**: Deterministic line-oriented ASCII records of state transitions.
   - **HBI (Hash-Based Index)**: Byte-exact random access index mapping sector, tick, byte offset, and record length.
   - **Trust Anchor (`.anchor`)**: Cryptographic signature binding total ticks, total rooms, and root SHA-256 digests for bit-for-bit verifiable replay.

### Native HTTP-0 96³ compute path and comparison boundary

The 2026-11-04 [engine release and prediction-first benchmark](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash/pull/3) adds **actual CPU state updates** on 23,887,872 trit channels, rather than expanding a virtual address catalog. Run `cargo +1.81.0 run --release --locked --offline -- --bench-engine 96 3` in the HTTP-0 repository. The [source-backed timing receipt](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash/blob/main/engine96/MEASURED-20261104.hbp) documents input-gate pinning, exact state reversal and recorded CPU times. The [Taylor–Green 96³ cutoff](https://github.com/JesseBrown1980/Taylor_green_regularity-resolved-and-solved/tree/main/results/2026-10-30-cutoff) is a different 192-step externally driven experiment with **C1 PASS / A1 FAIL**, retained on record.

**Storage distinction:** packed 8-byte Host8 rooms are one representation; the new mutable 96³ D3Q27 engine uses **47,775,744 bytes for two buffers**. The 23-billion and 3¹⁶ HTTP-0 identifiers are sparse **logical addresses**, not physical compute threads, GPU lanes or deployed network peers. On the recorded 24³ control the specialized old engine outperformed the generalized one, so there is no same-workload evidence of a general speed advantage over GPUs.

---

## 6. Repository Map & Cross-References

| Component | Repository | Source Path |
|---|---|---|
| **Host8 Disk Streaming** | `Clasy-repo-x-3-` | [`src/bin/sweep_rooms.rs`](https://github.com/JesseBrown1980/Clasy-repo-x-3-/blob/main/src/bin/sweep_rooms.rs) |
| **Fail-Closed Room Audit** | `Clasy-repo-x-3-` | [`src/bin/audit_rooms.rs`](https://github.com/JesseBrown1980/Clasy-repo-x-3-/blob/main/src/bin/audit_rooms.rs) |
| **D3Q27 Lattice Engine** | `finite-reversible-ternary-physics` | [`asolaria_equilibrium_suite.cpp`](https://github.com/JesseBrown1980/finite-reversible-ternary-physics/blob/main/asolaria_equilibrium_suite.cpp) |
| **Host8 Timing Benchmarks** | `finite-reversible-ternary-physics` | [`HOST8_LOCAL_PHYSICS_BENCHMARK_TIMINGS.md`](https://github.com/JesseBrown1980/finite-reversible-ternary-physics/blob/main/HOST8_LOCAL_PHYSICS_BENCHMARK_TIMINGS.md) |
| **300GB Substrate Proof** | `CORRECTION-TO-ASOLARIA...` | [`PROOF.md`](https://github.com/JesseBrown1980/CORRECTION-TO-ASOLARIA-AND-FAULT-TO-OPEN-AI-NAVIER-STOKES-SOLUTIONS-SOLVED/blob/main/PROOF.md) |
| **HTTP-0 Loopback Engine** | `qoled-internet-HEB-C-revisted...` | [`src/main.rs`](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash/blob/main/src/main.rs) |
| **Cross-Validation Receipts** | `qoled-internet-HEB-C-revisted...` | [`CROSS_VALIDATION_HOST8_HEBC_REPORT.md`](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash/blob/main/CROSS_VALIDATION_HOST8_HEBC_REPORT.md) |
| **Verified physical 96³ CPU engine** | `qoled-internet-HEB-C-revisted...` | [`src/scale96.rs`](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash/blob/main/src/scale96.rs) · [timings/receipt](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash/blob/main/engine96/MEASURED-20261104.hbp) |
| **Project announcement / source ledger** | `Hard-drive-and-USB-as-GPU` | [November 4 announcement](ANNOUNCEMENT-HTTP0-HOST8-WILLOW-20261104.md) · [October 24 HTTP-0 report](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash/blob/main/HEBC_23B_VIRTUAL_PORTAL_REPORT.md) |
| **Willow-class integer benchmark (10 runs)** | `Asolaria-vs-Williow-chip-Results` | [`RESULTS.md`](https://github.com/JesseBrown1980/Asolaria-vs-Williow-chip-Results/blob/main/RESULTS.md) · [primary HBP](https://github.com/JesseBrown1980/Asolaria-vs-Williow-chip-Results/blob/main/receipts/WILLOW-10RUNS-MAXTRITS-20261022.hbp) |
| **Willow-class 5-tier memory comparison** | `Asolaria-VS-GOOGLE-Willow-chip` | [`WILLOW-VS-ASOLARIA-REPORT.md`](https://github.com/JesseBrown1980/Asolaria-VS-GOOGLE-Willow-chip/blob/main/WILLOW-VS-ASOLARIA-REPORT.md) |
