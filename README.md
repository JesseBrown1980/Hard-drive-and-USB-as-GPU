# Hard Drive and USB Storage as Compute Substrate

Out-of-core memory addressing (Host8 / SG-RAM) and CPU integer streaming that replaces GPU VRAM allocations and cloud computing clusters across the Jesse Daniel Brown ecosystem.

---

## 1. Architectural Overview: Secondary Storage as Addressed Memory

Traditional deep learning, simulation, and scientific compute frameworks require tens to hundreds of gigabytes of expensive, dedicated GPU VRAM (e.g. H100/A100 clusters) and large system RAM pools. They rely heavily on floating-point general matrix multiplies (GEMM), incurring high memory bandwidth costs, cloud expenses, and PCIe bus transfer latency.

This repository documents the **Host8 / SG-RAM / Out-of-Core Architecture** established across Jesse Daniel Brown's codebase:
1. **Secondary Storage as Linear Memory**: High-capacity secondary storage (such as a 300 GB NVMe/SSD drive, local disk, or USB storage dock) is partitioned into fixed-size binary sector files and addressed directly via $O(1)$ linear byte offsets.
2. **CPU Integer Register Streaming**: Instead of loading hundreds of gigabytes into RAM or offloading to a GPU, lightweight CPU worker threads stream sequential windows through bounded, cache-friendly buffers (e.g. 4 MiB in CPU L3 cache).
3. **No GPU Required (`gpu_calls = 0`)**: All computational dynamics are formulated as exact integer permutations, discrete balanced-ternary gates, involutive collision operators ($U = U^{-1}$), or finite-field transforms. Standard CPU ALUs evaluate these discrete transitions faster than PCIe transfer overhead to an external GPU.

---

## 2. Core Repository Implementations

The architecture is implemented and verified across four primary repositories:

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

### D. [`qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash`](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash) *(Virtual Address Space & $0 Portal)*
- **Key Modules**:
  - `CROSS_VALIDATION_HOST8_HEBC_REPORT.md`: Physical 300 GB block execution and cross-executor verification.
  - `CANONICAL_RUST_HEBC_REPORT.md` & `REPRODUCE_NATIVE_RUST_181.md`: Headless, browser-independent execution with zero external cloud dependencies.
- **Virtual Memory Coprimality**:
  - Maps 23 billion logical process instances in $O(1)$ space using coprime hashing:
    $$\text{virtual\_id} = (\text{ordinal} \times 1,000,003) \pmod{23,000,000,000}$$
  - Unoccupied instances require **0 in-memory allocations**, allowing a machine with standard RAM and no GPU to achieve 28.2 million address probes/second.

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
