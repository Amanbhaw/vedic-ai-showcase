# Verifiable Edge AI — proof-carrying inference + cross-ISA determinism

A research showcase. **Results and a verifiable cryptographic proof are shared here; the
engine source, circuits, RTL and methodology are proprietary and intentionally withheld.**

---

## What this demonstrates (measured, not estimated)

| Result | Measured |
|---|---|
| **Zero-knowledge proof of a non-linear neural network on a $1 microcontroller** (bare-metal Cortex-M0 class) | **~2 KB RAM, 124-bit sound, non-interactive** |
| AI inference **bit-identical across x86-64, ARM64 and RISC-V** | **same hash on all three ISAs — verified in CI** |
| Real pretrained transformer (bert-tiny), integer-only engine | **cosine 0.9996 vs the float reference** |
| Image model (ResNet-18), integer vs FP32 on confident inputs | **98.1% agreement** |
| Zero-dependency inference engine footprint | **~35 KB** (vs 100s of MB / GBs for mainstream stacks) |
| Custom compute-tile silicon (SkyWater 130 nm), physical signoff | **DRC/LVS-clean, closed timing** |

Float AI stacks cannot produce a bit-identical result across chips (IEEE-754 addition isn't
associative), which is exactly what on-chain / zero-knowledge / safety-certified AI requires.
This engine is integer-only, so its output is reproducible everywhere — and small enough to
**prove its own computation on a dollar chip**.

## Cross-ISA determinism — proven in CI
Built and run for three different instruction-set architectures (x86-64 native, ARM64 and
RISC-V under emulation) on an independent cloud runner; all three produced the **identical**
64-bit checksum:

```
[x86_64 ]  0x94cb410e7fbb02ef
[aarch64]  0x94cb410e7fbb02ef
[riscv64]  0x94cb410e7fbb02ef
PROVEN — all three ISAs identical
```

## Verify the included proof yourself
The `proof/` folder contains a **real, verifiable zero-knowledge proof** (UltraHonk) with its
verification key and public inputs. You can check it with the standard verifier — it confirms
the computation is genuine **without revealing how the prover works**:

```bash
# Barretenberg (bb) — standard UltraHonk verifier
bb verify -p proof/proof -k proof/vk    # → "Proof verified successfully"
```

## Honest scope
- These are **engineering results**, built on established cryptography and integer math — **not
  a claim of new mathematics**, and not state-of-the-art-beating. The contribution is the
  combination, measured end-to-end, and the extreme footprint.
- Accuracy is an approximation (~1e-4 vs float); "bit-exact" means **across chips**, not to float.
- Full methodology, source, circuits and RTL are **proprietary and not published here.**

## Applications
Verifiable sensors (anti-fraud ESG / supply-chain / cold-chain), AI oracles for blockchains,
tamper-evident edge inference for safety- and defence-grade systems, and provenance-at-capture.

## Status & contact
Working prototypes, measured and CI-verified. Collaboration, licensing, grant and pilot
enquiries welcome — reach out via LinkedIn. **Full technical materials available under NDA.**

---
© 2026 — All rights reserved. See [LICENSE](LICENSE). No license is granted to use, copy, modify
or distribute any part of this work.
