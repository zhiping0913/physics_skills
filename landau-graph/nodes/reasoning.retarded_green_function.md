---
skill_id: reasoning.retarded_green_function
type: reasoning
summary_50t: >
  □A^i = (4π/c)j^i. Solution: retarded Green's function G_ret =
  δ(t−R/c)/R. Causality selects the retarded solution — outgoing waves.
trigger:
  - solving inhomogeneous wave equation
  - radiation from known source distribution
  - need to enforce causality in wave solutions
reasoning_role: causal_boundary_condition
parent: reasoning.causality_as_constraint
children:
  - knowledge.em.retarded_potentials
  - knowledge.em.lienard_wiechert
retrieval_cost: 1
---

# reasoning.retarded_green_function — Causality → Retarded Solution

## Core Picture

The wave equation □φ = −4πρ has two classes of solutions: retarded
(φ depends on ρ at earlier times) and advanced (depends on later times).
Causality selects retarded: φ(r,t) = ∫ ρ(r', t−R/c)/R dV'.

The reasoning: Lorentz gauge + Maxwell → □A^i = (4π/c)j^i.
Solve with point source δ(R) → φ = χ(t−R/c)/R.
Demand that near origin this reduces to Coulomb law → χ(t) = de(t).
→ φ = de(t−R/c)/R. Superpose: φ = ∫ ρ_{t−R/c}/R dV'.

## Algorithm

```
1. Apply Lorentz gauge ∂_i A^i = 0 to Maxwell equations
2. Obtain decoupled wave equations: □A^i = (4π/c)j^i
3. Seek particular solution for point source: ρ = de(t)δ(R)
4. Spherical symmetry + wave equation → φ = χ(t−R/c)/R
5. Determine χ by requiring Coulomb law at R→0: χ(t) = de(t)
6. General solution by superposition: φ = ∫ ρ(t−R/c)/R dV' + φ₀
7. φ₀, A₀ represent external incoming radiation
```

## Why Retarded, Not Advanced

For radiation FROM a system, the field at large distances must be an
OUTGOING wave ∝ f(t−R/c), not an incoming one ∝ f(t+R/c). The retarded
solution corresponds to the physical boundary condition that radiation
originates from sources and propagates outward.

## Key Insight

The retarded time t' = t − R/c means we "see" the source as it was
when the light was emitted. This is the mathematical expression of the
finite speed of light.

## Cross-References
- Landau Vol.2 §62 (retarded potentials)
- Landau Vol.2 §63 (Liénard-Wiechert — retarded potentials for point charge)
