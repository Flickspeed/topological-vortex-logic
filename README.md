# Topological Vortex Logic (TVL)

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.19682633.svg)](https://doi.org/10.5281/zenodo.19682633)
[![DOI - Software](https://zenodo.org/badge/DOI/10.5281/zenodo.19683377.svg)](https://doi.org/10.5281/zenodo.19683377)
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![Python 3.7+](https://img.shields.io/badge/python-3.7+-blue.svg)](https://www.python.org/)

---

## The Research

**T³ as a Closed Information-Processing Environment**
*Mathematical Requirements for Stable Discrete Information in a Compact Flat Manifold*
Vladimer Merebashvili — April 2026

**[→ Download the main paper (PDF)](https://doi.org/10.5281/zenodo.19682633)**
**[→ Download the technical derivation (PDF)](https://doi.org/10.5281/zenodo.19682633)**

### Abstract

We derive the minimal mathematical structures required for the three-dimensional flat
torus T³ = R³/LZ³ to function as a closed, stable, discrete information-processing
environment. The question is not what external physics the geometry implies, but what
the geometry itself requires: what conditions must hold for information to be stably
encoded, reliably clocked, conserved under flow, and filtered against noise within a
compact flat manifold with periodic boundary conditions.

We identify five minimal requirements — stability, a well-defined clock, conservation,
laminarity, and noise rejection — and show that each is satisfied by a unique
mathematical object that T³ provides automatically, without external design. The stable
information vocabulary consists of exactly 3³ − 1 = 26 discrete vortex states in three
symmetry families determined by the first Betti number b₁(T³) = 3. The natural clock
is the lowest cavity resonance f₁ = c/L. Information is conserved by seven independent
quantities: four continuous Noether charges and three discrete topological winding
numbers. Laminar flow is the unique consequence of the Laplace equation on a compact
flat manifold. Noise rejection operates at two complementary levels: the Landau
energetic filter and Legendre's three-square theorem.

### The Five Theorems

1. **Stability** (CLEAN): A vortex state w in Z³ is stable if and only if |w|² ≤ 3.
2. **Z₃ Invariant** (CLEAN): The charge q₃ = (w₁+w₂+w₃) mod 3 is a topological invariant from the T³/Z₃ orbifold holonomy.
3. **A₂ Root Embedding** (CLEAN): The six traceless edge vortices form the A₂ root geometry of su(3).
4. **Non-Isomorphism** (CLEAN): The three vortex families are pairwise non-isomorphic as Z₃-modules.
5. **Mandatory Hierarchy** (CONDITIONAL): The non-isomorphism forces any coupling sensitive to the Z₃-module structure to treat the three families unequally.

### SAP Labels

| Label | Meaning |
|-------|---------|
| `CLEAN` | Derived from T³/Z₃ geometry alone. Zero external input. |
| `IMPORTED` | Uses the single external QCD identification (B = ±1/3). |
| `CONDITIONAL` | Geometry plus an additional coupling assumption. |
| `WALL` | Open boundary requiring physics beyond the current framework. |

---

## The Papers

Both papers are archived permanently at Zenodo:

> **Main paper** — T³ as a Closed Information-Processing Environment (18 pages)
> Merebashvili, V. (2026). Zenodo. https://doi.org/10.5281/zenodo.19682633

> **Technical report** — Topological Vortex Logic: Complete Derivation (12 pages)
> Full proofs of all five theorems with worked examples. Code available separately via software DOI.
> Merebashvili, V. (2026). Zenodo. https://doi.org/10.5281/zenodo.19682633

Version history:
- v1.0.1 (current): https://doi.org/10.5281/zenodo.19688501
- v1.0.0 (original): https://doi.org/10.5281/zenodo.19682634

---

## The Software — TVL.py

`TVL.py` is the standalone computational engine for the TVL framework. It implements
all five theorems, classifies any winding vector, and verifies every result in the
papers through 44 self-test assertions. No external dependencies — requires only Python 3.7+.

The software is separately archived at: https://doi.org/10.5281/zenodo.19683377

### Quick Start

```bash
python TVL.py              # run self-test + B₃ verification + module invariants
python TVL.py --all        # print all 26 stable states
python TVL.py --map        # print full map including unstable states
python TVL.py 1,0,0        # classify a specific winding vector
```

```python
from TVL import TVL

TVL.classify((1, 0, 0))     # face / gen 1 / q₃=1 / B=+1/3 / quark
TVL.classify((1, 1, 1))     # corner / gen 3 / q₃=0 / B=0 / lepton
TVL.classify((1, -1, 0))    # edge / q₃=0 / A₂ root / gluon
TVL.classify((1, 1, -1))    # corner / exotic (color-6, open wall)
TVL.classify((2, 0, 0))     # UNSTABLE (splits favorably)
```

### Key Methods

```python
TVL.all_stable()              # dict of all 26 stable states
TVL.closed_form_stable(w)     # algebraic stability proof for any w
TVL.verify_b3_root_system()   # verify all 4 B₃ axioms + Cartan matrix
TVL.print_module_invariants() # Z₃-module non-isomorphism table
```

### Self-Test

```
Running TVL self-test (44 assertions)...
  OK  26 stable states total
  OK  6  face vortices
  OK  12 edge vortices
  OK  8  corner vortices
  ...
All 44 assertions passed.

B₃ ≅ so(7): ALL AXIOMS PASS ✓
```

---

## Repository Structure

```
TVL.py                        — standalone Python framework (no dependencies)
README.md                     — this file
T3_Information_Processing_Environment.pdf — main paper (18 pages)
TVL_Complete_Derivation.pdf   — technical report with proofs (12 pages)
```

---

## Framework Summary

| Property | Value | Source |
|----------|-------|--------|
| Stable vocabulary | 26 = 3³ − 1 states | Landau stability on T³ |
| Family structure | 3 families (6 + 12 + 8) | b₁(T³) = 3 |
| Fourth generation | Forbidden | Theorem 1 |
| Z₃ charge partition | 8 singlets / 9 quarks / 9 antiquarks | T³/Z₃ holonomy |
| Symmetry group | O_h, order 48 | Cubic lattice symmetry |
| Root system (face+edge) | B₃ ≅ so(7), 18 roots | Cartan matrix |
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
| First forbidden shell | |n|² = 7 | Legendre |
| Addressing capacity | log₂(26) ≈ 4.70 bits | 26-state vocabulary |
| Spin structures | 8 = 2³ | H¹(T³, Z₂) ≅ Z₂³ |
| External inputs | B = ±1/3 only | One QCD identification |
| Open walls | Exotic sector, electroweak, mass magnitudes | Pending Paper 2 |

---

## Citation

**Cite the papers as:**
Merebashvili, V. (2026). *Topological Vortex Logic: Stable Winding States on the Three-Torus and Their Classification*. Zenodo. https://doi.org/10.5281/zenodo.19682633

**Cite the code as:**
Merebashvili, V. (2026). *Topological Vortex Logic (TVL): Python Framework* (v1.0.1). Zenodo. https://doi.org/10.5281/zenodo.19683377

---

## Acknowledgements

The author thanks Dr. Z. Merebashvili for careful reading of the manuscript and for
identifying the inconsistency in Section 4 regarding the incommensurability of the
shell frequencies f₁, f₂, and f₃.

---

## Changelog

### v1.0.2 (April 2026)
**T3_Information_Processing_Environment.pdf**
- DOI on title page updated to Concept DOI (10.5281/zenodo.19682633)
- References reordered [1]–[8] to match order of first citation in text
- Appendix headers properly titled: "Appendix A — Verification of the B₃ Root System" and "Appendix B — Legendre's Three-Square Theorem"

**TVL_Complete_Derivation.pdf**
- DOI on title page updated to Concept DOI (10.5281/zenodo.19682633)
- Appendix C code listing removed; replaced with pointer to standalone software record (doi.org/10.5281/zenodo.19683377)
- Paper reduced from 23 to 12 pages

### v1.0.1 (April 2026)
- ℏ defined as reduced Planck constant at first use (§3.2)
- h defined as Planck's constant at first use (§5.1)
- c defined as characteristic signal propagation speed at first use (§4.2)
- §4.4 corrected: f₁, f₂, f₃ are mutually incommensurate; f₁ is the master clock
- All key display equations numbered (10 in main paper, 13 in technical report)
- Acknowledgements section added

### v1.0.0 (April 21, 2026)
- Initial release

## License

© Vladimer Merebashvili, 2026.
Licensed under [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).
You are free to share and adapt this work with appropriate credit.
