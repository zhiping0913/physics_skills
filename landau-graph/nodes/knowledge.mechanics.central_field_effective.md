---
skill_id: knowledge.mechanics.central_field_effective
type: knowledge
summary_50t: >
  In central field U(r), angular momentum conservation reduces 2D motion
  to 1D radial motion with U_eff = U(r) + M²/2mr². The centrifugal barrier
  term prevents fall to center unless U(r) is singular enough.
trigger:
  - central force problem → use U_eff
  - analyzing turning points of orbits
reasoning_role: effective_potential_reduction
parent: reasoning.conservation_to_effective_reduction
related:
  - knowledge.mechanics.kepler_problem
retrieval_cost: 1
---

# knowledge.mechanics.central_field_effective

**Key equation**:
```
E = (m/2)ṙ² + U_eff(r),  U_eff(r) = U(r) + M²/(2mr²)
dr/dt = ±√[(2/m)(E − U_eff(r))]
dφ = (M/mr²) dt → φ = ∫ (M/r²)dr / √[2m(E−U) − M²/r²]
```

**Turning points**: U_eff(r) = E → ṙ = 0. Between r_min and r_max.

**Trajectory closure**: Δφ = rational × 2π. Only U ∝ −1/r and U ∝ r²
give all closed orbits (Bertrand's theorem).

**Fall to center condition**: r²U(r) → −∞ faster than −M²/2m as r→0.

**Geometric meaning**: M = 2m ḟ where ḟ = sectorial velocity (area/time).
Kepler's 2nd law: dA/dt = M/2m = const.

- Landau Vol.1 §14
