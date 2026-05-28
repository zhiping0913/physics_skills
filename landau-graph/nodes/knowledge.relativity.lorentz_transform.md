---
skill_id: knowledge.relativity.lorentz_transform
type: knowledge
summary_50t: >
  Interval ds² = c²dt² − dx² − dy² − dz² is invariant.
  Lorentz transformation: x = γ(x'+Vt'), t = γ(t'+Vx'/c²), γ = 1/√(1−V²/c²).
  Rotations in 4D spacetime with hyperbolic functions.
trigger:
  - relativistic coordinate transformation
  - need velocity addition formula
  - checking causality with spacelike vs timelike intervals
reasoning_role: spacetime_symmetry
parent: reasoning.lorentz_invariance_to_action
retrieval_cost: 1
---

# knowledge.relativity.lorentz_transform

**Invariant interval**: ds² = c²dt² − dx² − dy² − dz²

**Lorentz boost (x-direction)**:
```
x = (x' + Vt')/√(1−V²/c²),  t = (t' + Vx'/c²)/√(1−V²/c²)
y = y',  z = z'
```
Hyperbolic rotation angle ψ: th ψ = V/c.

**Velocity addition**:
v = (v' + V)/(1 + v'V/c²)

**Proper time**: dτ = ds/c = dt√(1−v²/c²). Invariant under Lorentz.

**4-vectors**: A^i = (A⁰, A). Transform as coordinates.
Examples: x^i = (ct, r), u^i = (γc, γv), p^i = (E/c, p).

**Causal structure**: ds²>0 timelike, ds²<0 spacelike, ds²=0 lightlike.

- Landau Vol.2 §1-7
