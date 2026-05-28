---
skill_id: reasoning.conservation_to_effective_reduction
type: reasoning
summary_50t: >
  A conservation law can reduce the effective dimensionality of a problem.
  Angular momentum conservation → effective 1D radial motion with U_eff.
  Cyclic coordinates → conserved p → eliminate that DOF.
trigger:
  - system with known conserved quantity
  - need to reduce dimensionality
  - central force problem
reasoning_role: dimensional_reduction
parent: reasoning.symmetry_to_conservation
children:
  - knowledge.mechanics.kepler_problem
related:
  - knowledge.mechanics.cyclic_coordinate
retrieval_cost: 1
---

# reasoning.conservation_to_effective_reduction — Conservation → Dimension Reduction

## Core Picture

Every conserved quantity eliminates one dynamical variable. Angular momentum
conservation in a central field collapses 2D motion to 1D radial motion under
U_eff = U(r) + M²/2mr². The centrifugal barrier term M²/2mr² is not a real
force — it is the kinetic energy of angular motion, repackaged as an effective
potential term.

## Algorithm

```
1. Identify conserved quantity (M, p_φ, etc.)
2. Express the eliminated coordinate's velocity in terms of the conserved quantity
3. Substitute into the energy integral
4. The result is a 1D energy equation with an effective potential:
   E = (m/2)q̇² + U_eff(q) where U_eff absorbs the conserved quantity
5. Analyze turning points: U_eff(q) = E → bounds of motion
6. Extract the trajectory: dq/dt = ±√[(2/m)(E − U_eff(q))]
```

## The Cyclic Coordinate Variant

If L doesn't contain qᵢ → pᵢ = ∂L/∂q̇ᵢ = const.
Then qᵢ is eliminated, and the remaining s−1 DOF problem has
one fewer variable. This is the simplest form of dimensional reduction.

## Trajectory Closure

For central field: Δφ = 2∫(M/r²)dr/√[2m(E−U) − M²/r²].
If Δφ/2π = m/n (rational), trajectory is closed.
Closed orbits — Bertrand's theorem: Only U ∝ −1/r and U ∝ r² give
strictly closed orbits for all bound states. This is a THEOREM requiring
proof (perturbation analysis of Δφ around circular orbit). The node
states the result; see Vol.1 §14 appendix for the full derivation.

## Edge Cases

- **Fall to center**: If r²U(r) → −∞ faster than −M²/2m as r→0,
  the centrifugal barrier is overcome.
- **M = 0**: No angular momentum → pure radial motion, U_eff = U(r).

## Cross-References

- Landau Vol.1 §14 (Central field)
- Plasma: guiding center reduction (μ-conservation → effective 1D along B)
- Quantum: radial Schrödinger equation uses same U_eff
