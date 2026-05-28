---
skill_id: knowledge.em.field_tensor
type: knowledge
summary_50t: >
  F_ik = ∂_iA_k − ∂_kA_i. Antisymmetric 4-tensor unifying E and H.
  E = (F_01, F_02, F_03), H = (F_23, F_31, F_12).
  Invariants: F_ik F^{ik} = 2(H²−E²), e^{iklm}F_ikF_lm ∝ E·H.
trigger:
  - expressing EM fields in covariant form
  - Lorentz transformation of E, H fields
  - constructing gauge-invariant quantities
reasoning_role: field_unification
parent: reasoning.gauge_invariance_to_field_tensor
children:
  - knowledge.em.maxwell_from_action
retrieval_cost: 1
---

# knowledge.em.field_tensor

**Definition**: F_ik = ∂_iA_k − ∂_kA_i, where A^i = (φ, A)

**Matrix form** (row=i, col=k):
```
     [ 0   E_x  E_y  E_z]
F =  [−E_x  0   −H_z  H_y]
     [−E_y H_z   0   −H_x]
     [−E_z −H_y H_x   0 ]
```

**Dual tensor**: *F^{ik} = ½ e^{iklm} F_lm (swap E↔−H, H↔E)

**Lorentz invariants**:
```
F_ik F^{ik} = 2(H² − E²)          invariant
e^{iklm} F_ik F_lm ∝ E·H          invariant (pseudoscalar)
```

**Field transformation** (boost along x):
```
E'_x = E_x,        E'_y = γ(E_y − VH_z/c),  E'_z = γ(E_z + VH_y/c)
H'_x = H_x,        H'_y = γ(H_y + VE_z/c),  H'_z = γ(H_z − VE_y/c)
```

**Key insight**: E and H are NOT separate entities — they are components
of one tensor. What is pure E in one frame becomes mixed E+H in another.

- Landau Vol.2 §23-25
