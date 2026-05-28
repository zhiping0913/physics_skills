---
skill_id: reasoning.microcanonical_to_canonical
type: reasoning
summary_50t: >
  For a small subsystem of a large closed system: w_n ∝ exp(−E_n/T).
  Derived by expanding S'(E^(0)−E_n) = S'(E^(0)) − E_n/T + ...
  Temperature emerges as dS/dE = 1/T.
trigger:
  - deriving the canonical (Gibbs) distribution
  - connecting microcanonical (fixed E) to canonical (fixed T) ensemble
  - subsystem of a much larger system at equilibrium
reasoning_role: ensemble_equivalence
parent: reasoning.ensemble_logic
children:
  - knowledge.statistical.gibbs_distribution
retrieval_cost: 1
---

# reasoning.microcanonical_to_canonical — Closed System → Subsystem Distribution

## Core Picture

Total closed system: energy E^(0) fixed. Microcanonical distribution:
dw ∝ δ(E + E' − E^(0)) dΓ dΓ'.

Body (subsystem) has energy E_n. Environment has energy E' = E^(0) − E_n.
Probability w_n = const · (e^{S'(E')}/ΔE') at E' = E^(0) − E_n.

Key move: E_n ≪ E^(0) (body is small) → expand:
S'(E^(0) − E_n) = S'(E^(0)) − E_n ∂S'/∂E^(0) + ...

But ∂S/∂E = 1/T (defines temperature). Thus:
w_n = A exp(−E_n/T)

## Algorithm

```
1. Write microcanonical for total system: dw = const · δ(E+E'−E^(0)) dΓ dΓ'
2. Integrate over environment DOF: w_n = const · ∫ δ(E_n+E'−E^(0)) dΓ'
3. Replace dΓ' = (dΓ'/dE') dE' = [e^{S'(E')}/ΔE'] dE'
4. δ-function picks E' = E^(0) − E_n
5. Small subsystem → expand S'(E^(0)−E_n) to linear order in E_n
6. w_n ∝ exp[−E_n/T], where T defined by 1/T = dS/dE
7. Z = Σ exp(−E_n/T) (partition sum), A = 1/Z
```

## Why Temperature Emerges

Temperature is NOT a primitive. It is DEFINED by 1/T = ∂S/∂E.
This is the statistical definition: temperature measures how entropy
responds to energy input. Hotter systems gain less entropy per unit energy.

## Edge Cases

- System NOT small compared to environment: expansion fails → need
  full microcanonical treatment
- Long-range interactions: entropy may not be additive
- Quantum degeneracy (T ~ T_F): classical expansion still works,
  but E_n includes quantum level structure

## Cross-References
- Landau Vol.5 §28 (Gibbs distribution)
- Landau Vol.5 §7 (entropy definition, S = ln ΔΓ)
- Landau Vol.5 §9 (temperature)
