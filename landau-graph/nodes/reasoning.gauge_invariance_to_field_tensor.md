---
skill_id: reasoning.gauge_invariance_to_field_tensor
type: reasoning
summary_50t: >
  The potentials A_i are not unique (A_i → A_i + ∂_iχ gives same physics).
  → The action cannot depend on A_i directly → must use the gauge-invariant
  field tensor F_ik = ∂_iA_k − ∂_kA_i. All physical quantities are built from F_ik.
trigger:
  - constructing a field theory with gauge redundancy
  - need to identify physical observables in a gauge theory
  - A_i appears but is not unique → find invariant combination
reasoning_role: gauge_redundancy_resolution
parent: reasoning.symmetry_drives_physics
children:
  - knowledge.em.field_tensor
retrieval_cost: 1
---

# reasoning.gauge_invariance_to_field_tensor — Gauge Redundancy → Physical Fields

## Core Picture

The 4-potential A^i = (φ, A) is not unique. The transformation
A_i → A_i + ∂_iχ leaves the physics unchanged for any scalar χ.

This means A_i itself cannot appear in the action for the field S_f —
only gauge-invariant combinations can. The simplest such combination
is the antisymmetric derivative: F_ik = ∂_iA_k − ∂_kA_i.

The field tensor F_ik IS the electromagnetic field. E and H are its components.

## Algorithm

```
1. Identify gauge freedom: A_i → A_i + ∂_iχ leaves EOM unchanged
2. Conclude: A_i cannot appear directly in the field action S_f
3. Construct simplest gauge-invariant combination from derivatives of A_i
4. F_ik = ∂_iA_k − ∂_kA_i (antisymmetric → 6 independent components)
5. E = (F_01, F_02, F_03),  H = (F_23, F_31, F_12)
6. All physical quantities must be expressible in terms of F_ik alone
```

## In the Action

The particle-field interaction CAN use A_i because it appears under
an integral along the worldline where the gauge term ∫ dχ integrates
to boundary values (zero for closed paths or fixed endpoints):
S_mf = −(e/c)∫ A_i dx^i.

But the FIELD action S_f must depend on F_ik: S_f ∝ ∫F_ik F^{ik} dΩ.

## Key Insight

Gauge invariance isn't a bug — it's a feature that FORCES the theory
to have the right structure. It reduces the 4 apparent degrees of freedom
in A_i to the 2 physical polarizations of EM waves.

## Cross-References
- Landau Vol.2 §18 (gauge invariance), §23 (field tensor), §27 (field action)
- Modern: gauge principle is the foundation of all fundamental interactions
- **Gauge invariance → charge conservation**: The footnote to §18 notes that
  gauge invariance and charge conservation (∂_μ j^μ = 0) are two aspects
  of the same underlying principle — Noether's theorem applied to the
  U(1) gauge symmetry of electromagnetism.
