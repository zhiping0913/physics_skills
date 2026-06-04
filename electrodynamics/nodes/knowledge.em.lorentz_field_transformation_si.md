---
skill_id: knowledge.em.lorentz_field_transformation_si
type: knowledge
summary_50t: >
  SI Lorentz transform: E'_∥=E_∥, E'_⊥=γ(E+v×B)_⊥; B'_∥=B_∥,
  B'_⊥=γ(B−v×E/c²)_⊥. F^μν SI matrix with E/c rows. Invariants:
  F^μνF_μν=2(B²−E²/c²), ε^μνρσF_μνF_ρσ∝E·B/c. Bridge from Gaussian.
trigger:
  - need to transform E,B between inertial frames in SI units
  - computing fields in moving media or relativistic particle interactions
  - bridging landau-graph Gaussian field tensor to SI downstream skills
retrieval_cost: 1
---

# knowledge.em.lorentz_field_transformation_si — E,B Under Boost in SI

## Core Picture

Electromagnetic fields transform under Lorentz boosts. The SI form differs
from the Gaussian/landau-graph form by explicit factors of c and by using
B (magnetic flux density) rather than H. This node restates the transformation
in project SI convention for direct use by `electrodynamics`, `plasma`, and
`optics` skills without needing a bridge conversion each time.

## Field Transformation (SI)

For a boost with velocity v along x:

```
E'_x = E_x                          B'_x = B_x
E'_y = γ(E_y − v B_z)               B'_y = γ(B_y + v E_z / c²)
E'_z = γ(E_z + v B_y)               B'_z = γ(B_z − v E_y / c²)
```

Vector form (boost velocity v, arbitrary direction):

```
E'_∥ = E_∥                          B'_∥ = B_∥
E'_⊥ = γ (E + v × B)_⊥              B'_⊥ = γ (B − v × E / c²)_⊥
```

where γ = 1/√(1−v²/c²), ∥ and ⊥ refer to components parallel/perpendicular to v.

## F^μν Matrix in SI

With metric (−,+,+,+) and coordinates x^μ = (ct, x, y, z):

```
           [   0        E_x/c    E_y/c    E_z/c ]
F^μν  =    [ −E_x/c       0       B_z      −B_y ]
           [ −E_y/c     −B_z       0        B_x ]
           [ −E_z/c      B_y      −B_x       0   ]

F_μν  =    [   0       −E_x/c   −E_y/c   −E_z/c ]
           [  E_x/c       0       B_z      −B_y ]
           [  E_y/c     −B_z       0        B_x ]
           [  E_z/c      B_y      −B_x       0   ]
```

Under Lorentz transform Λ: F'^μν = Λ^μ_ρ Λ^ν_σ F^ρσ.

## Lorentz Invariants (SI)

```
F^μν F_μν = 2(B² − E²/c²)                    (scalar)
(1/4) ε^μνρσ F_μν F_ρσ = −2 E·B / c         (pseudoscalar)
```

where ε^μνρσ is the Levi-Civita symbol (ε^0123 = +1).

## Bridge from landau-graph (Gaussian → SI)

`landau-graph: knowledge.em.field_tensor` gives the field transformation in
Gaussian form using H (magnetic field strength). Conversion to project SI:
- Replace H → B/μ₀ in all transformation formulas
- Add explicit 1/c² factors on E terms in B' transformation
- F^μν in Gaussian has E components without 1/c factor → add in SI
- The Jacobian ∂(E,B)/∂(E',B') of the transformation is identical in both
  systems (the Lorentz boost matrix is unit-system-independent)

Reference: `physics-conventions: exceptions.landau_graph_bridge` for
general conversion rules; this node is the explicit worked instance.

## Edge Cases

- **Low-velocity limit** (v ≪ c): γ ≈ 1 → E' ≈ E + v×B, B' ≈ B − v×E/c².
  The v×E/c² term in B' is O(v/c) but matters when E is large (e.g., intense
  laser fields in plasma: E ∼ 10¹² V/m → v×E/c² ∼ 10 T at v/c=0.1).
- **Purely electric field in one frame**: In frame S: (E, B=0). In boosted
  frame: B' = −γ v×E/c² ≠ 0. A moving observer sees a MAGNETIC field from
  a static charge distribution (origin of motional EMF).
- **Purely magnetic field**: In S: (E=0, B). Boosted: E' = γ v×B. Moving
  conductor in B → motional EMF.

## Cross-References

- Jackson §11.9-11.10, Cao §5.39, §5.44, §5.48
- landau-graph: knowledge.em.field_tensor (Gaussian form, parent)
- landau-graph: reasoning.gauge_invariance_to_field_tensor (4-vector formulation)
- physics-conventions: exceptions.landau_graph_bridge (Gaussian→SI conversion)
