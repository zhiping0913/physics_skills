---
name: mathematics-theorems
description: "Mathematical infrastructure for physics skills: vector/dyadic algebra, Green's identities (scalar→vector→dyadic hierarchy), plane wave spectrum, Sommerfeld integrals, steepest descent asymptotics, plus theorem proofs (Bertrand, Liouville-Arnold, Airy asymptotics). Extended with IEEE Press Series (Tai 1993/1997, Clemmow 1996, Felsen & Marcuvitz 1994)."
---

# Mathematics Theorems Repository

Mathematical reasoning templates and theorem proofs used by `landau-graph`,
`electrodynamics`, `plasma`, `optics`, and future `computational-physics` skills.

## Node Categories

### Reasoning Nodes (IEEE Press Phase 1 — 2026-06-05)

| Node | Content | Source |
|------|---------|--------|
| `mathematics.dyadic_algebra` | Dyadic definition, products (dot, cross, double-dot), classification (symmetric/antisymmetric), unit dyadic, inverse, spectral decomposition | Tai (VDA) §1-5-1-7, §7 |
| `mathematics.vector_green_identities` | Scalar→Vector→Dyadic Green's identities hierarchy. Stratton-Chu formula. Divergence theorem → Huygens principle → equivalence principle | Tai (VDA) §4-9-4-10, §7-2 |
| `mathematics.plane_wave_spectrum` | 2D Fourier representation of EM fields. Propagating vs evanescent spectra. Weyl identity. Angular spectrum of beams | Clemmow (1996) |
| `mathematics.sommerfeld_integral` | Sommerfeld identity. Branch cuts and Riemann sheets. Surface/leaky wave poles. Layered media Green's functions | Chew (1999) §2, Felsen & Marcuvitz §5 |
| `mathematics.steepest_descent` | Saddle point method. SDP deformation. Leading-order asymptotic. EM applications: far-field radiation, Cherenkov cone, leaky waves | Felsen & Marcuvitz §4 |

### Theorem Reference Nodes (existing)

| Theorem | Used in | File |
|---------|---------|------|
| Bertrand's theorem | landau-graph: `conservation_to_effective_reduction` | `references/bertrand-theorem.md` |
| Liouville-Arnold theorem | landau-graph: `separation_of_variables` | `references/liouville-arnold.md` |
| Distribution limits | landau-graph: `quantum_perturbation_theory` | `references/distribution-limits.md` |
| Airy function asymptotics | landau-graph: `wkb_quasiclassical` | `references/airy-asymptotics.md` |
| 4D δ-function Jacobian | landau-graph: `retarded_green_function` | `references/delta-function-4d.md` |

## External Prerequisites

The following are standard undergraduate mathematics topics — referenced as
`parent:` edges but not distilled as independent nodes:
- `mathematics.vector_algebra` — dot/cross products, grad/div/curl, Stokes/Gauss theorems
- `mathematics.fourier_transform` — 1D/2D/3D Fourier transforms, convolution
- `mathematics.complex_analysis` — analytic functions, contour integration, residue theorem

## Source Texts (IEEE Press Series)

- Tai, *General Vector and Dyadic Analysis* (2nd ed., 1997)
- Tai, *Dyadic Green Functions in Electromagnetic Theory* (2nd ed., 1993)
- Clemmow, *The Plane Wave Spectrum Representation of EM Fields* (1996)
- Felsen & Marcuvitz, *Radiation and Scattering of Waves* (1994)
- Chew, *Waves and Fields in Inhomogeneous Media* (1999)
- Lindell, *Multiforms, Dyadics, and Electromagnetic Media* (2015)
