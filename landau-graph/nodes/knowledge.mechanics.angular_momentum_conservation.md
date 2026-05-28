---
skill_id: knowledge.mechanics.angular_momentum_conservation
type: knowledge
summary_50t: >
  Space isotropy → M = Σ rₐ×pₐ conserved. For central field,
  M = mr²φ̇ = const (Kepler's 2nd law: equal areas in equal times).
trigger:
  - rotationally symmetric system → M conserved
  - central field → M conserved about center
reasoning_role: conserved_quantity
parent: reasoning.symmetry_to_conservation
retrieval_cost: 1
---

# knowledge.mechanics.angular_momentum_conservation

**Equation**: M = Σ rₐ×pₐ = Σ mₐ(rₐ×vₐ)

**Derivation**: Infinitesimal rotation δr = δφ×r. δL = 0 → dM/dt = 0.

**Coordinate expression**: M_z = Σ mₐrₐ²φ̇ₐ (in cylindrical coords).
M_z = ∂L/∂φ̇ when φ is rotation angle.

**Center-of-mass decomposition**: M = M_int + R×P, where M_int is the
angular momentum in the CM frame.

**Validity**: All 3 components in closed system. In central field: all 3
about the center. In axially symmetric field: M_z conserved.

**Connection**: M conservation → motion in a plane → 2D reduced to 1D
(see reasoning.conservation_to_effective_reduction).

- Landau Vol.1 §9
