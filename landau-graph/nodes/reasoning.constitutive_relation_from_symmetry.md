---
skill_id: reasoning.constitutive_relation_from_symmetry
type: reasoning
summary_50t: >
  Viscous stress σ'_ik must be: (1) linear in ∂v_i/∂x_k, (2) zero for
  rigid rotation, (3) isotropic. These three constraints uniquely determine
  σ'_ik = η(∂v_i/∂x_k + ∂v_k/∂x_i − 2/3 δ_ik div v) + ζδ_ik div v.
trigger:
  - constructing constitutive relations for continuous media
  - need stress tensor for fluid, elastic solid, plasma
  - symmetry + linearity → unique form
reasoning_role: constitutive_closure
parent: reasoning.continuum_limit_to_field_equations
children:
  - knowledge.fluid.navier_stokes
retrieval_cost: 1
---

# reasoning.constitutive_relation_from_symmetry — Symmetry + Linearity → Unique Form

## Core Picture

The viscous stress tensor σ'_ik cannot be derived from first principles
alone — it requires a CONSTITUTIVE relation (a model of the material).
But symmetry arguments dramatically constrain its form:

1. Linearity: for small velocity gradients, σ'_ik ∝ ∂v_i/∂x_k
2. Galilean invariance: σ'_ik = 0 for uniform translation (v = const)
3. Rotational invariance: σ'_ik = 0 for rigid rotation (v = Ω×r)
4. Isotropy: the tensor structure must be built from δ_ik only

These four constraints leave exactly TWO free parameters (η, ζ).

## Algorithm
```
1. Start from ideal momentum flux tensor (§7): Π_ik = pδ_ik + ρv_i v_k
   Euler equation: ∂(ρv_i)/∂t = −∂Π_ik/∂x_k
   Viscous fluid: add σ'_ik → Π_ik = pδ_ik + ρv_i v_k − σ'_ik
2. Write σ'_ik = A_iklm ∂v_l/∂x_m (linearity)
3. Demand σ'_ik = 0 when v = Ω×r → ∂v_i/∂x_k + ∂v_k/∂x_i vanishes
   → A_iklm must be symmetric in i,k
4. Isotropy: A_iklm = η(δ_il δ_km + δ_im δ_kl) + (ζ − 2η/3)δ_ik δ_lm
5. Result: σ'_ik = η(∂v_i/∂x_k + ∂v_k/∂x_i − 2/3 δ_ik ∂v_l/∂x_l) + ζδ_ik ∂v_l/∂x_l
6. η > 0, ζ > 0 (dissipation must increase entropy — 2nd law)
```

## The Two Viscosities

η: shear viscosity (trace-free part). ζ: bulk (second) viscosity (trace part).
For incompressible flow (div v = 0), only η matters. For compressible
flow (sound waves, shocks), ζ matters too.

## Navier-Stokes

ρ(∂v/∂t + v·∇v) = −∇p + η∇²v + (ζ+η/3)∇(div v).

## Cross-References
- Landau Vol.6 §15 (Navier-Stokes derivation)
- Landau Vol.7: elasticity theory uses the SAME reasoning
  (symmetry → unique form of elastic modulus tensor)
- Landau Vol.8: MHD adds magnetic stress tensor (same pattern)
