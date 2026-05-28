---
skill_id: knowledge.mechanics.hamilton_jacobi
type: knowledge
summary_50t: >
  ∂S/∂t + H(q, ∂S/∂q, t) = 0. S(q,α,t) is the action as a function
  of endpoint. When separable → s conserved αᵢ → complete integrability.
trigger:
  - seeking a canonical transformation that makes H' = 0
  - testing whether a system is integrable
reasoning_role: action_as_generator
parent: knowledge.mechanics.hamilton_equations
children:
  - knowledge.mechanics.action_angle_variables
retrieval_cost: 1
---

# knowledge.mechanics.hamilton_jacobi

**The equation**: ∂S/∂t + H(q₁,...,q_s, ∂S/∂q₁,..., ∂S/∂q_s) = 0

**For conservative systems**:
```
S(q,α,t) = S₀(q,α) − E(α)t
S₀ satisfies: H(q, ∂S₀/∂q) = E
```

**Complete integral**: Solution with s independent constants α₁,...,α_s.
Differentiating ∂S/∂αᵢ = βᵢ (new constants) yields the trajectory.

**Physical meaning**: S is the generator of a canonical transformation
to constant variables. ∂S/∂q = p (momentum). ∂S/∂t = −H (energy).

**When separable** (see reasoning.separation_of_variables):
H-J decomposes into s ODEs → system is completely integrable.

- Landau Vol.1 §47-48
