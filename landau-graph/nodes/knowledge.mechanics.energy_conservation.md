---
skill_id: knowledge.mechanics.energy_conservation
type: knowledge
summary_50t: >
  Time homogeneity → ∂L/∂t = 0 → E = Σ q̇ᵢ pᵢ − L is constant.
  For natural systems L = T − U, E = T + U.
trigger:
  - closed system or constant external field
  - checking energy balance
reasoning_role: conserved_quantity
parent: reasoning.symmetry_to_conservation
retrieval_cost: 1
---

# knowledge.mechanics.energy_conservation — Energy Conservation

## Key Equation
```
E = Σ q̇ᵢ ∂L/∂q̇ᵢ − L
  = T + U  (when L = T − U, T quadratic in q̇)
```

## Derivation
dL/dt = Σ(∂L/∂qᵢ q̇ᵢ + ∂L/∂q̇ᵢ q̈ᵢ) + ∂L/∂t.
If ∂L/∂t = 0 and using E-L: d/dt(Σ q̇ᵢ ∂L/∂q̇ᵢ − L) = 0.

## Validity
- Closed systems: always
- System in CONSTANT external field: yes (∂L/∂t = 0)
- Time-dependent external field: E is NOT conserved

## Cross-References
- Landau Vol.1 §6
