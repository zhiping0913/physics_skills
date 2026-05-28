---
skill_id: knowledge.statistical.gibbs_distribution
type: knowledge
summary_50t: >
  Canonical: w_n = exp(−E_n/T)/Z, Z = Σ exp(−E_n/T).
  Classical: ρ(p,q) = exp(−E(p,q)/T)/Z. Gibbs 1901.
  Maxwell: p-distribution ~ exp(−p²/2mT) independent of interactions.
trigger:
  - equilibrium distribution for subsystem
  - computing thermal averages
  - all of equilibrium statistical mechanics
reasoning_role: canonical_ensemble
parent: reasoning.microcanonical_to_canonical
children:
  - knowledge.statistical.free_energy
retrieval_cost: 1
---

# knowledge.statistical.gibbs_distribution

**Canonical (Gibbs)**: w_n = A exp(−E_n/T), A = 1/Z, Z = Σ exp(−E_n/T).

**Classical**: ρ(p,q) = A exp(−E(p,q)/T), ∫ ρ dp dq = 1.
K ∝ p² → momentum distribution independent of interactions.
**Maxwell distribution**: dw_p ∝ exp(−p²/2mT) d³p.

**Key property**: For macroscopic body, E-fluctuation is negligible
(ΔE/E ~ 1/√N). Canonical ≈ microcanonical for all practical purposes.

**Applicable to closed bodies**: Statistical properties of a closed body
are the same whether treated as closed or as subsystem of thermostat,
except for total energy fluctuations (which are fictitious for closed body).

- Landau Vol.5 §28-29
