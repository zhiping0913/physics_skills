---
skill_id: knowledge.statistical.entropy
type: knowledge
summary_50t: >
  S = ln ΔΓ = −Σ w_n ln w_n. Statistical weight ΔΓ = number of microstates.
  Entropy is additive, non-negative, and measures disorder.
  dS/dE = 1/T defines temperature.
trigger:
  - need statistical definition of entropy
  - connecting microstates to thermodynamics
  - checking entropy change in a process
reasoning_role: microscopic_origin_of_entropy
parent: reasoning.ensemble_logic
retrieval_cost: 1
---

# knowledge.statistical.entropy

**Definition**:
```
S = ln ΔΓ          (statistical weight)
S = −Σ w_n ln w_n  (Gibbs entropy formula)
S = −∫ ρ ln[(2πℏ)^s ρ] dp dq  (classical)
```

**Properties**: Additive (S = Σ S_a), non-negative (ΔΓ ≥ 1).
Without ℏ, classical entropy has ambiguous additive constant.
ℏ fixes the unit cell (2πℏ)^s in phase space → makes S absolute.

**Temperature**: 1/T = ∂S/∂E. Statistical definition — temperature is
NOT a fundamental quantity but a derived concept from entropy.

**Law of increase**: For closed system, entropy increases to maximum
at equilibrium (2nd law of thermodynamics).

- Landau Vol.5 §7, §8
