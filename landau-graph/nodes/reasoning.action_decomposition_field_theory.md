---
skill_id: reasoning.action_decomposition_field_theory
type: reasoning
summary_50t: >
  S = S_field + S_matter + S_interaction. Field equations come from varying
  S_f; matter equations from S_m; interaction couples them. This triple
  decomposition is universal for all field theories.
trigger:
  - constructing a field theory from action principle
  - system with field + particles/charges
  - need to derive coupled field-matter equations
reasoning_role: field_theory_construction
parent: reasoning.variational_principle
children:
  - knowledge.em.maxwell_from_action
  - knowledge.em.energy_momentum_tensor_field
retrieval_cost: 1
---

# reasoning.action_decomposition_field_theory — Triple Decomposition of Action

## Core Picture

For ANY field theory with matter, the total action splits into three parts:
```
S = S_f + S_m + S_mf
```
S_f: field alone (quadratic in field variables → linear field equations)
S_m: matter alone (free particles/fields without interaction)
S_mf: interaction term (couples field to matter — linear in field)

This decomposition is universal: EM, Yang-Mills, gravity, all follow it.

## Application to EM (Vol.2 §27)

```
S_f   = −(1/16πc)∫ F_ik F^{ik} dΩ     field action (E²−H²)/8π
S_m   = −Σ mc∫ ds                      free particle action
S_mf  = −Σ (e/c)∫ A_k dx^k            interaction (charge × potential)
```

## Key Reasoning Steps

1. **S_f must be quadratic**: Superposition principle (sum of two solutions is
   a solution) → field equations must be LINEAR → action must be quadratic.
2. **S_f must be gauge-invariant**: Cannot contain A_i directly → must be
   function of F_ik. Only scalar from F_ik is F_ik F^{ik}.
3. **S_f must contain (∂A/∂t)² with + sign**: Otherwise the action could be
   made arbitrarily negative by rapid time variation of A → no minimum exists.
   This fixes a = −1/(16π) in Gaussian units.
4. **Pseudoscalar excluded automatically**: ε^{iklm}F_{ik}F_{lm} is a total
   4-divergence, so adding it to the action does not change the field equations.
5. **S_mf must be linear in A_i**: To couple charge to field. The term
   (e/c)A_k dx^k is the simplest Lorentz scalar coupling charge to potential.

## Universal Pattern

| Theory | S_f | S_m | S_mf |
|--------|-----|-----|------|
| EM | F² | particle -mc∫ds | e∫A·dx |
| Scalar (Klein-Gordon) | (∂φ)² − m²φ² | — | gφψ̄ψ |
| Gravity (Einstein) | R√(−g) | matter −mc∫ds | g_μν couples to T^{μν} |

## Cross-References
- Landau Vol.2 §27 (action for EM field)
- Landau Vol.2 §93 (action for gravitational field)
