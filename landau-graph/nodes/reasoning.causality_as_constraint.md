---
skill_id: reasoning.causality_as_constraint
type: reasoning
summary_50t: >
  Response cannot precede cause. This single physical principle
  forces analyticity of response functions in the upper half-plane,
  selects retarded over advanced solutions, and underlies the
  fluctuation-dissipation theorem.
trigger:
  - selecting physical solution from mathematically equivalent alternatives
  - analytic structure of response functions
  - relation between dissipation and fluctuations
reasoning_role: causality_principle
parent: reasoning.variational_principle
children:
  - reasoning.retarded_green_function
  - reasoning.causality_to_analyticity
  - reasoning.fluctuation_dissipation_quantum
retrieval_cost: 1
---

# reasoning.causality_as_constraint — Causality Drives Physics

## Core Picture

"Effect cannot precede cause" seems obvious — but it has profound
mathematical consequences when applied to field theory and statistical
mechanics:

1. Response functions must vanish for negative times → f(τ)=0 for τ<0
2. This forces ε(ω) to be analytic in the upper half-plane → Kramers-Kronig
3. For wave equations with sources, it selects the retarded solution over
   the advanced one → radiation propagates OUTWARD
4. Combined with thermal/quantum averaging → fluctuation-dissipation theorem

Causality is not just a philosophical principle — it is a MATHEMATICAL
CONSTRAINT that determines the form of physical laws.

## Three Instances

| Volume | Application | What Causality Determines |
|--------|------------|--------------------------|
| Vol.2 §62 | Retarded potentials | φ = ∫ ρ_{t-R/c}/R dV (not advanced) |
| Vol.8 §77,82 | Kramers-Kronig | Re ε(ω) ↔ Im ε(ω) via Hilbert transform |
| Vol.9 §122 | Fluctuation-dissipation | ⟨x²⟩ ↔ χ''(ω) via coth(ℏω/2T) |

## The Deep Connection

All three are the SAME mathematical structure: the response function
χ(t) vanishes for t<0 → χ(ω) is analytic in UHP → Cauchy integral
gives relations between real and imaginary parts.

## Cross-References
- reasoning.retarded_green_function (Vol.2)
- reasoning.causality_to_analyticity (Vol.8)
- reasoning.fluctuation_dissipation_quantum (Vol.9)
