---
skill_id: knowledge.statistical.equipartition
type: knowledge
summary_50t: >
  Each quadratic degree of freedom contributes T/2 to ⟨E⟩.
  ⟨p_i²/2m⟩ = T/2, ⟨mω²q_i²/2⟩ = T/2. Classical only (T ≫ ℏω).
  Specific heat: c_V = (f/2)R for ideal gas (f DOF per molecule).
trigger:
  - classical estimate of energy per DOF
  - heat capacity of ideal gas
  - checking whether quantum effects matter
reasoning_role: energy_distribution
parent: knowledge.statistical.gibbs_distribution
retrieval_cost: 1
---

# knowledge.statistical.equipartition

**Theorem**: For classical system, any variable x appearing quadratically
in E (as Ax²) contributes T/2 to the mean energy.

**Proof**: ⟨Ax²⟩ = ∫ Ax² exp(−Ax²/T) dx / ∫ exp(−Ax²/T) dx = T/2.

**Applications**:
- Monatomic gas: 3 translational DOF → ⟨E⟩ = (3/2)T, c_V = (3/2)R.
- Diatomic gas: +2 rotational → c_V = (5/2)R (classical).
  +1 vibrational → c_V = (7/2)R (only at high T, when ℏω ≪ T).
- Crystalline solid: 3N harmonic oscillators → c_V = 3R (Dulong-Petit).

**Failure at low T**: When T ≪ ℏω, the DOF "freezes out."
The transition from classical (c_V constant) to quantum (c_V → 0 as T→0)
is the central problem of low-temperature thermodynamics.

- Landau Vol.5 §44
