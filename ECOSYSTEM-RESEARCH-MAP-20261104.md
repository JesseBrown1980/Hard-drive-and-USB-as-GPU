# Cross-repository research map — QNN, Google circuits, HTTP-0, Host8, Yang–Mills and Willow

**Updated November 4, 2026.** This is the reverse-navigation index for the work described across the project discussions. All repository targets listed here were checked to exist on GitHub before writing this map. Links to some unpublished reviews remain intentionally outside the release record.

## Most recent results, traced backwards

| Workstream | Repository and source-of-record | What is established | Next check |
|---|---|---|---|
| Google same-gate test | [QNN / GGUF models](https://github.com/JesseBrown1980/GGUF-files-operating-as-trained-quantum-neural-network-models) · [complete 24-qubit 1,257-gate PR #5](https://github.com/JesseBrown1980/GGUF-files-operating-as-trained-quantum-neural-network-models/pull/5) · [official Google qsim source comparison PR #6](https://github.com/JesseBrown1980/GGUF-files-operating-as-trained-quantum-neural-network-models/pull/6) | **Source-matched Google qsim PASS:** complete 1,257-gate sample, 64 complex amplitudes/128 components within 10⁻⁶, maximum difference 1.667×10⁻⁹; wrong-√Y mutant 128/128 components rejected. [Official hosted HBP](https://github.com/JesseBrown1980/GGUF-files-operating-as-trained-quantum-neural-network-models/blob/main/docs/GOOGLE-QSIM-OFFICIAL-REFERENCE-20261104.hbp) | Full Willow 103-qubit source-specific experiment is a further benchmark |
| HTTP-0 native compute | [HEB-C/HTTP-0 main](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash) · [96³ merge #3](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash/pull/3) · [measured HBP](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash/blob/main/engine96/MEASURED-20261104.hbp) | 23,887,872 physically updated ternary D3Q27 channels, old 24³ byte equality and three-step reversal; 3¹⁶ sparse evidence addresses remain separate | Driven Taylor–Green replay |
| HTTP-0 quantum register experiment | [Qutrit integration PR #5](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash/pull/5) · [prediction-first source](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash/blob/fable5-qutrit-96cubed-20261104/qutrit/PREDICTION.hbp) | 23,887,872 three-level channels run in 183 s on one CPU, with branch-by-branch reversible lattice engine, phase register; 16-qutrit exact-addressable 3¹⁶-amplitude interference cycle reports 1.999463 | PR #5 hosted seven checks PASS; independent second-seat attack pending before merge |
| HTTP-0 virtual-source bridge | [source catalog](https://github.com/JesseBrown1980/qoled-internet-HEB-C-revisted-HTTP---free-0-hbi-hbp-sha-sh-hash/blob/main/docs/HTTP0-YANG-MILLS-3POWER16.md) · [YM #108](https://github.com/JesseBrown1980/Finite-universe-Yang-mills-existence-and-mass-gap-using-HEB-C/pull/108) · [audit #112](https://github.com/JesseBrown1980/Finite-universe-Yang-mills-existence-and-mass-gap-using-HEB-C/pull/112) | 43,046,721-address virtual ternary space, 729 Clay/Taylor observations and 3 source-backed YM receipts, tamper and collision rejection | Full 3×4 physics remains separate |
| Finite Yang–Mills CI | [finite Yang–Mills main](https://github.com/JesseBrown1980/Finite-universe-Yang-mills-existence-and-mass-gap-using-HEB-C) · [whole test campaign #111](https://github.com/JesseBrown1980/Finite-universe-Yang-mills-existence-and-mass-gap-using-HEB-C/pull/111) | All registered Rust, 11 cloud replays and five finite 2×2 dual-route jobs passed; same-workload HTTP-0 compute speedup not established | 3×4 full-row/pair reruns on pinned sector store; gap verdict OPEN |
| 4D transfer operator and locality | [4D Yang–Mills project](https://github.com/JesseBrown1980/yang-mills-4-dimensional-continum-proof) · [YM4 #22](https://github.com/JesseBrown1980/yang-mills-4-dimensional-continum-proof/pull/22) · [YM4-02e draft #26](https://github.com/JesseBrown1980/yang-mills-4-dimensional-continum-proof/pull/26) | Finite transfer-operator quantitative gap merged; **YM4-02e base locality Theorem 5 independently proof-reviewed at `6322746`**, all 10 checks PASS and frozen receipt unchanged | Operator/maintainer draft merge decision; sharper SU(2) and physical-spacing research tracked separately |
| Taylor–Green physical source | [Taylor–Green project](https://github.com/JesseBrown1980/Taylor_green_regularity-resolved-and-solved) · [2026-10-30 cutoff](https://github.com/JesseBrown1980/Taylor_green_regularity-resolved-and-solved/tree/main/results/2026-10-30-cutoff) · [HTTP-0 link #4](https://github.com/JesseBrown1980/Taylor_green_regularity-resolved-and-solved/pull/4) | Physically simulated 96³ cutoff; C1 conservation PASS and A1 amplitude FAIL preserved | Exact full driven 192-step replay |
| Clay bridge | [Continuum Clay variation](https://github.com/JesseBrown1980/continuum-Clay-variation) · [3-leaf bridge PR #3](https://github.com/JesseBrown1980/continuum-Clay-variation/pull/3) | Exact 81 register projections over 3 arms and 3 ticks, source hashes and nonlinear mismatch preserved | Nonlinear map equivalence remains OPEN |

## Earlier components these experiments reuse

| Component | Repository | Concrete role |
|---|---|---|
| Asolaria QNN v1–v11 | [GGUF quantum neural network models](https://github.com/JesseBrown1980/GGUF-files-operating-as-trained-quantum-neural-network-models) | Exact qutrit/rational/GGUF Yang–Mills lattice-state models; now contains separately scoped exact-qubit Google tests |
| Multi-model GGUF | [Mixed-GGUFs, Asolaria, Mythos and Kimi](https://github.com/JesseBrown1980/Mixed-GGUFs-as-the-neural-networks-using-asolaria-star-and-mythos-and-kimi) | GGUF model pairing and related upstream file/workflow research |
| Host8 C++ physics | [Finite reversible ternary physics](https://github.com/JesseBrown1980/finite-reversible-ternary-physics) | Source D3Q27 kernel and source-defined collision/invariant controls |
| Host8 / Clasy | [Clasy X3](https://github.com/JesseBrown1980/Clasy-repo-x-3-) | Storage-linked classical kernel and finite physics results |
| Read-only storage/USB | [Hard-drive-and-USB-as-GPU](https://github.com/JesseBrown1980/Hard-drive-and-USB-as-GPU) | Present out-of-core storage and mapped CPU-workload architecture, announcement and links |
| OS/runtime federation | [Asolaria Argon OS](https://github.com/JesseBrown1980/Asolaria-Argon-Antigravity-Unification-ASI-OS) | Rust 1.81 core, Host8 mapped storage and USB station-dock federation |
| Willow-class test reports | [Asolaria-vs-Williow-chip-Results](https://github.com/JesseBrown1980/Asolaria-vs-Williow-chip-Results) · [five-tier report](https://github.com/JesseBrown1980/Asolaria-VS-GOOGLE-Willow-chip) · [12.5B suite](https://github.com/JesseBrown1980/Asolaria-12.5-B-full-power-vrs-Willow-Chip) | Classical 108-lane integer transforms, mapped-memory speeds, exact syndrome benchmarks; not demonstrated same-gate Willow fidelity |
| SU(N) finite gauge extensions | [Finite-Universe-SU-N-solved](https://github.com/JesseBrown1980/Finite-Universe-SU-N-solved) | Z3/S3/Q8/2T/2O finite-group transfer and Hamiltonian test outcomes |
| Quantum observation registries | [Hidden model-state observations](https://github.com/JesseBrown1980/AAAAAAAAAAAAAA-Quantum-observations-of-hidden-model-states) | Historical operator observations and quantum-state experiment records; distinct from physical qubit implementations |
| Stone/moss experimental branch | [asolaria-stone-to-moss](https://github.com/JesseBrown1980/asolaria-stone-to-moss) | Related stored and recorded research artifacts |

## Shared proof and measurement vocabulary

- **Physical computation** counts values actually updated and measured, including input data size and total memory. For example, 96³×27=23,887,872 mutable trits in the CPU engine.
- **Virtual addresses** count locations a formula could index. The earlier HTTP-0 browser example reported 23 billion possible IDs with 1,990,656 *actual probes*; the 3¹⁶ catalog has 43,046,721 possible positions, **732 occupied evidence entries**.
- **Exact qubits** require the original quantum gate operators and amplitudes or statistically validated circuit output distributions. A qutrit, ternary channel, GGUF register or virtual address is not a qubit.
- **Evidence/source audit** verifies pinned hashes and recorded integer fields. It does not reexecute a large Yang–Mills Hamiltonian.
- **PASS/FAIL/HOLD/OPEN** refer to the registered prediction and exact test scope. Prior failed predictions and interrupted runs are retained, never converted into successes after correction.

## Starting points

- [Public announcement: HTTP-0 + Host8 + Willow](ANNOUNCEMENT-HTTP0-HOST8-WILLOW-20261104.md)
- [QNN Google same-circuit test documentation](https://github.com/JesseBrown1980/GGUF-files-operating-as-trained-quantum-neural-network-models/blob/main/docs/GOOGLE-QSIM-LIKE-FOR-LIKE-20261104.md)
- [Google qsim input format](https://quantumai.google/qsim/input_format)
- [Google Willow published system metrics](https://quantumai.google/site-assets/downloads/willow-spec-sheet.pdf)

**Repository-navigation policy:** these are source links and independently registered programs, not a statement that all programs form one binary or implement the same physical theory. Future evidence merges should update both this map and the producing repository's own README.
