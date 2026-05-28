---
skill_id: knowledge.mechanics.momentum_conservation
type: knowledge
summary_50t: >
  Space homogeneity → P = Σ mₐvₐ conserved. Generalized momentum
  pᵢ = ∂L/∂q̇ᵢ conserved when qᵢ is cyclic.
trigger:
  - closed system
  - field symmetric in a direction → that P component conserved
reasoning_role: conserved_quantity
parent: reasoning.symmetry_to_conservation
related:
  - knowledge.mechanics.cyclic_coordinate
retrieval_cost: 1
---

# knowledge.mechanics.momentum_conservation — Momentum Conservation

## Key Equation
```
P = Σ pₐ = Σ mₐvₐ   (Cartesian)
pᵢ = ∂L/∂q̇ᵢ        (generalized, conserved if qᵢ cyclic)
```

## Center of Mass
For closed system, R = Σ mₐrₐ / Σ mₐ moves uniformly.
Internal energy E_int = E − μV²/2.

## Validity
- Closed system: all 3 components conserved
- Homogeneous field along z: P_x, P_y conserved, P_z not
- Overall: Σ Fₐ = 0 for closed system (action = reaction)

## Cross-References
- Landau Vol.1 §7, §8
