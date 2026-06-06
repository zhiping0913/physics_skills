---
name: computational-physics
description: "Computational electromagnetics and physics simulation methods: Method of Moments (MoM), Finite Element Method (FEM), FDTD Yee algorithm, TLM, multigrid solvers, PML absorbing boundary conditions, and numerical modal expansions. Distilled from IEEE Press Series on Electromagnetic Wave Theory."
unit_system: SI
conventions: >
  See `physics-conventions` for all sign/normalization/naming defaults.
  Time-harmonic convention: e^{−iωt} (physics). Spatial step: Δx, Δy, Δz.
  Stability conditions use Courant number CFL. Matrix assembly uses
  sparse formats (CSR/CSC). All algorithms assume linear, time-invariant,
  isotropic media unless stated otherwise.
---

# Computational Physics — CEM Methods

Constructive reasoning templates for numerical solution of Maxwell's equations
and wave problems. Every node gives a concrete algorithm: "Given geometry,
material parameters, and excitation → assemble discrete system → solve →
extract physical observables."

## Source Texts (IEEE Press Series)

- Harrington, *Field Computation by Moment Methods* (1993)
- Peterson, Ray & Mittra, *Computational Methods for Electromagnetics* (1997)
- Volakis, Chatterjee & Kempel, *Finite Element Method Electromagnetics* (1998)
- Christopoulos, *The Transmission-Line Modeling Method* (1995)
- Zhu & Cangellaris, *Multigrid FEM for Electromagnetic Field Modeling* (2006)
- Sevgi, *Electromagnetic Modeling and Simulation* (2014)
- Kast et al., *Advances in Time-Domain Computational EM Methods* (2022)

## Node Types

- **Reasoning nodes**: Procedural algorithms — "Given X, do Y, get Z."
- **Knowledge nodes**: Reference data (stability limits, basis function catalogs,
  PML parameters, common pitfalls).
