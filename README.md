# Topological Vortex Logic (TVL)

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.19682634.svg)](https://doi.org/10.5281/zenodo.19682634)
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![Python 3.7+](https://img.shields.io/badge/python-3.7+-blue.svg)](https://www.python.org/)

**A complete computational framework for classifying stable winding states on the three-torus T³.**

This repository contains `TVL.py` — the standalone implementation of the TVL classification map derived in:

> **T³ as a Closed Information-Processing Environment**  
> Vladimer Merebashvili, April 2026.  
> DOI: [10.5281/zenodo.19682634](https://doi.org/10.5281/zenodo.19682634)

and the companion technical report:

> **Topological Vortex Logic: Complete Derivation**  
> Vladimer Merebashvili, April 2026.  
> DOI: [10.5281/zenodo.19682634](https://doi.org/10.5281/zenodo.19682634)

Both papers and the code are archived at Zenodo:  
**https://doi.org/10.5281/zenodo.19682634**

---

## What is TVL?

The three-torus T³ = ℝ³/LZ³ equipped with a Z₃ orbifold symmetry supports exactly **26 stable vortex states** — the non-zero elements of {−1, 0, 1}³. These states organise into three families determined by how many of the three topological winding channels are simultaneously active:

| Shell | \|w\|² | Count | Generation | Physical sector |
|-------|--------|-------|------------|-----------------|
| Face  | 1 | 6  | 1st | Quarks / antiquarks |
| Edge  | 2 | 12 | 2nd | Quarks / antiquarks / gluons |
| Corner| 3 | 8  | 3rd | Leptons / exotic |

The classification is derived from geometry alone. The only external input is the assignment of baryon number B = ±1/3 from QCD (one identification, clearly labelled `IMPORTED`). Everything else — stability, Z₃ charge, SU(3) representation, sector — follows from T³/Z₃ topology with zero free parameters.

---

## Requirements

Python 3.7 or later. No external dependencies — only the standard library (`fractions`, `itertools`, `dataclasses`).

```bash
python TVL.py        # runs self-test + B₃ verification + module invariants
```

---

## Quick Start

```python
from TVL import TVL

# Classify any winding vector
TVL.classify((1, 0, 0))
# w=(1, 0, 0)  |w|²=1  shell=face  gen=1  q₃=1  B=1/3  rep=3 (fundamental)  sector=quark

TVL.classify((1, -1, 0))
# w=(1,-1, 0)  |w|²=2  shell=edge  gen=2  q₃=0  B=  0  rep=A₂ root (gluon)  sector=gluon (SU(3) gauge)

TVL.classify((1, 1, 1))
# w=(1,  1, 1)  |w|²=3  shell=corner  gen=3  q₃=0  B=0  rep=singlet  sector=lepton

TVL.classify((1, 1, -1))
# w=(1,  1,-1)  |w|²=3  shell=corner  gen=3  q₃=1  B=1/3  rep=6 (sym tensor)  sector=exotic (color-6, open wall)

TVL.classify((2, 0, 0))
# w=(2, 0, 0)  |w|²=4  UNSTABLE  (splits favorably — forbidden generation)
```

---

## The Complete Stable Vocabulary

```python
TVL.print_all()         # all 26 states grouped by shell
TVL.print_full_map()    # all states with |w|² ≤ 6, including unstable
```

```
── FACE  |w|²=1 ──────────────────────────────────────────
w=  (1, 0, 0)  |w|²=1  shell=face  gen=1  q₃=1  B= 1/3  rep=3 (fundamental)   sector=quark
w=  (0, 1, 0)  |w|²=1  shell=face  gen=1  q₃=1  B= 1/3  rep=3 (fundamental)   sector=quark
w=  (0, 0, 1)  |w|²=1  shell=face  gen=1  q₃=1  B= 1/3  rep=3 (fundamental)   sector=quark
w= (-1, 0, 0)  |w|²=1  shell=face  gen=1  q₃=2  B=-1/3  rep=3̄ (antifund)      sector=antiquark
w=  (0,-1, 0)  |w|²=1  shell=face  gen=1  q₃=2  B=-1/3  rep=3̄ (antifund)      sector=antiquark
w=  (0, 0,-1)  |w|²=1  shell=face  gen=1  q₃=2  B=-1/3  rep=3̄ (antifund)      sector=antiquark

── EDGE  |w|²=2 ──────────────────────────────────────────
  (6 gluon states with q₃=0, traceless — the A₂ root system of SU(3))
  (3 quark edge states, 3 antiquark edge states)

── CORNER  |w|²=3 ────────────────────────────────────────
w=  (1, 1, 1)  |w|²=3  shell=corner  gen=3  q₃=0  B=  0  rep=singlet   sector=lepton
w= (-1,-1,-1)  |w|²=3  shell=corner  gen=3  q₃=0  B=  0  rep=singlet   sector=lepton
  (6 exotic corner states — rep-6, open wall)
```

---

## Key Methods

### Classification

```python
state = TVL.classify((1, 0, 0))

state.stable        # True
state.shell         # 'face'
state.generation    # 1
state.q3            # 1
state.B             # Fraction(1, 3)
state.su3_rep       # '3 (fundamental)'
state.sector        # 'quark'
state.sap_label     # 'IMPORTED'  (because B=±1/3 uses external QCD identification)
state.to_dict()     # all fields as a plain dict
```

### Stability proof (Theorem 1)

```python
TVL.closed_form_stable((2, 1, 0))
# {
#   'stable': False,
#   'norm2': 5,
#   'reason': '|w|²=5 ≥ 4. Component w[0]=2 has |w[0]|≥2.
#              Choose s=(1,0,0): w·s=2 ≥ 2 > 1 = |s|².
#              Split is favorable. Residual ws=(1,1,0), |ws|²=2.
#              Energy: 5ε₀ → (1+2)ε₀ = 3ε₀.',
#   'split_s': (1, 0, 0),
#   'w_dot_s': 2
# }
```

### Z₃-module invariants (Theorem 3 — Non-Isomorphism)

The three families are pairwise non-isomorphic as Z₃-modules. This is proved computationally by comparing fixed-point counts and ρ₀ multiplicities under the cyclic permutation g: (w₁,w₂,w₃) → (w₂,w₃,w₁):

```python
TVL.print_module_invariants()

# Z₃-Module Invariants (Theorem 3 — Non-Isomorphism)
# ──────────────────────────────────────────────────────
#   Family      N  Fixed pts    ρ₀    ρ₁    ρ₂  Uniform
#   ──────────────────────────────────────────────────────
#   face        6          0     2     2     2      Yes
#   edge       12          0     4     4     4      Yes
#   corner      8          2     4     2     2     No ←
#
#   Face vs Corner: fixed_pts 0 ≠ 2  → not isomorphic ✓
#   Edge vs Corner: fixed_pts 0 ≠ 2  → not isomorphic ✓
#   Face vs Edge:   ρ₀         2 ≠ 4  → not isomorphic ✓
```

### B₃ root system verification (Appendix A)

```python
TVL.verify_b3_root_system()

# Axiom 1 — closure under negation:           ✓
# Axiom 2 — no non-±1 multiples:              ✓
# Axiom 3 — integer Cartan entries (306 pairs):✓
# Axiom 4 — reflection closure:               ✓
# Cartan matrix (simple roots):               ✓
#   computed  = [[2, -1, 0], [-1, 2, -2], [0, -1, 2]]
#   expected  = [[2, -1, 0], [-1, 2, -2], [0, -1, 2]]
# Weyl group order: 3!×2³ = 48 = |O_h|  ✓
# B₃ ≅ so(7): ALL AXIOMS PASS ✓
```

---

## Self-Test

```bash
python TVL.py
```

Runs 44 assertions covering vocabulary counts, individual vector classifications, SAP labels, the closed-form stability proof, the B₃ root system verification, and the Z₃-module non-isomorphism invariants. All must pass before any result in the papers should be trusted.

```
Running TVL self-test (44 assertions)...

  OK  26 stable states total
  OK  6  face vortices
  OK  12 edge vortices
  OK  8  corner vortices
  ...
  OK  corner fixed_pts=2
  OK  face   rho0=2
  OK  edge   rho0=4
  OK  corner rho0=4

All 44 assertions passed.
```

---

## SAP Labels

Every classification carries an epistemic status label:

| Label | Meaning |
|-------|---------|
| `CLEAN` | Derived from T³/Z₃ geometry alone. Zero external input. |
| `IMPORTED` | Uses the single external QCD identification (B = ±1/3 from baryon number). |
| `WALL` | Open boundary. Requires physics beyond the current T³/Z₃ framework to resolve. |

The exotic sector (rep-6 corner states) is labelled `WALL`: these states are stable and coloured, but their physical identity requires coupling to the full gauge algebra — a result not yet derived within this framework.

---

## Command-Line Usage

```bash
# Run full self-test (default)
python TVL.py

# Print all 26 stable states
python TVL.py --all

# Print full map including unstable states up to |w|²=6
python TVL.py --map

# Classify specific vectors
python TVL.py 1,0,0
python TVL.py 1,1,1  0,-1,1  2,0,0
```

---

## Repository Structure

```
TVL.py                        — the complete framework (no dependencies)
README.md                     — this file
t3_info_paper.pdf             — main paper (18 pages)
TVL_Complete_Derivation.pdf   — technical report with proofs (23 pages)
```

All files are also permanently archived at:  
**https://doi.org/10.5281/zenodo.19682634**

---

## Framework Summary

| Property | Value | Source |
|----------|-------|--------|
| Stable vocabulary | 26 = 3³ − 1 states | Landau stability on T³ |
| Family structure | 3 families (6 + 12 + 8) | b₁(T³) = 3 |
| Fourth generation | Forbidden | Theorem 1 |
| Z₃ charge partition | 8 singlets / 9 quarks / 9 antiquarks | T³/Z₃ holonomy |
| Symmetry group | O_h, order 48 | Cubic lattice symmetry |
| Root system (face+edge) | B₃ ≅ so(7), 18 roots | Cartan matrix (Appendix A) |
| A₂ root system (gluons) | 6 traceless edge states | Traceless projection |
| Non-isomorphism | Three families pairwise distinct | Theorem 3 |
| Fundamental clock | f₁ = c/L = c/(2πR) | T³ cavity eigenspectrum |
| Time quantum | t_q = L/c | Inverse clock frequency |
| Conservation laws | 7 total (4 Noether + 3 topological) | Noether + π₁(T³) = Z³ |
| Error gap | ε₀ (topological winding threshold) | Energy model |
| Flow type | Laminar, uniform geodesic | K=0 + Laplace on T³ |
| Information latency | ≤ √3 · t_q | T³ geometry |
| Landau filter | Decays |w|² > 3 within t_q | E(nw) = n²E(w) |
| Legendre filter | Forbidden shells 4ᵃ(8b+7) | Three-square theorem |
| First forbidden shell | \|n\|² = 7 | Legendre |
| Addressing capacity | log₂(26) ≈ 4.70 bits | 26-state vocabulary |
| Spin structures | 8 = 2³ | H¹(T³, Z₂) ≅ Z₂³ |
| External inputs | B = ±1/3 only | One QCD identification |
| Open walls | Exotic sector, electroweak, mass magnitudes | Pending Paper 2 |

---

## License

© Vladimer Merebashvili, 2026.  
Licensed under [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).  
You are free to share and adapt this work with appropriate credit.

**Cite as:**  
Merebashvili, V. (2026). *Topological Vortex Logic: Stable Winding States on the Three-Torus and Their Classification* (1.0.0). Zenodo. https://doi.org/10.5281/zenodo.19682634
