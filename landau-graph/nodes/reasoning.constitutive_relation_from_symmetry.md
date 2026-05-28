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

- Landau Vol.6 §15 (Navier-Stokes viscous stress derivation)
- **Cross-volume trinity**: The SAME template (linearity + symmetry →
  unique tensor) applies in THREE physically different contexts:
  1. **Viscous stress** (Vol.6 §15): σ'_ik = η(∂_i v_k + ∂_k v_i − ⅔δ_ik div v) + ζδ_ik div v
  2. **Hooke's law** (Vol.7 §4): σ_ik = K u_ll δ_ik + 2μ(u_ik − ⅓δ_ik u_ll)
     — Two elastic constants for isotropic body because only two independent
     quadratic scalar invariants from the strain tensor.
  3. **Dielectric tensor** (Vol.8 §103): D_i = ε_ik E_k classified by crystal symmetry
  4. **Conductivity** (Vol.10): j_i = σ_ik E_k — same symmetry classification
- In ALL cases: the form of the constitutive tensor is determined by
  (a) linearity of response, (b) symmetry of the medium, (c) Onsager
  reciprocity. The rank and index structure differ, but the reasoning
  is identical.
- This is arguably the single most powerful cross-volume transfer pattern
  in the entire Landau course — mastering it once gives you the key to
  fluid dynamics, elasticity, electrodynamics of continuous media, and
  transport theory.
