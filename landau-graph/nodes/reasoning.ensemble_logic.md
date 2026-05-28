---
skill_id: reasoning.ensemble_logic
type: reasoning
summary_50t: >
  Replace a single deterministic trajectory with an ensemble of identical
  systems. Each member has probability w_n = exp(−E_n/T)/Z. This is the
  fundamental bridge from mechanics to thermodynamics.
trigger:
  - need to describe a system with ~10²³ degrees of freedom
  - macroscopic observables as ensemble averages
  - when deterministic prediction is impossible or irrelevant
reasoning_role: statistical_ensemble
parent: reasoning.variational_principle
children:
  - knowledge.statistical.gibbs_distribution
  - knowledge.statistical.entropy
  - knowledge.statistical.free_energy
retrieval_cost: 1
---

# reasoning.ensemble_logic — Deterministic → Probabilistic Description

## Core Picture

Classical mechanics says: given (q,p) at t=0, the future is determined.
But for 10²³ particles, we cannot know (q,p). And we don't need to —
macroscopic observables are averages over astronomically many microstates.

The move: replace the system with an ENSEMBLE — infinitely many copies,
distributed in phase space according to a probability distribution ρ(q,p).
Macroscopic quantities = ensemble averages ⟨f⟩ = ∫ f ρ dΓ.

This is not an approximation. It is a different LEVEL of description.
Landau: "Statistical physics is not 'less rigorous' than mechanics —
it is a logically closed system built on its own foundations."

## The Gibbs Method

1. The system is in equilibrium → ρ depends only on integrals of motion
2. For a subsystem of a large closed system: ρ ∝ exp(−E/T) (canonical)
3. The constant T (temperature) is the parameter characterizing the environment
4. All thermodynamics follows from Z = Σ exp(−E_n/T) → F = −T ln Z

## Why This Works

The distribution is SHARP. For a macroscopic body, the energy fluctuation
ΔE/E ~ 1/√N. The system spends virtually all time at E ≈ ⟨E⟩.
The ensemble average equals the time average (ergodic hypothesis).

## Key Insight

The Gibbs distribution is NOT assumed — it is DERIVED.
Starting from the microcanonical ensemble for the total closed system,
treating the body as a small subsystem, and expanding the environment's
entropy S'(E^(0)−E_n) to linear order → w_n ∝ exp(−E_n/T).

This is Landau's signature: every distribution is a consequence of more
fundamental principles, never an axiom.

## Cross-References
- Landau Vol.5 §1-7 (basic principles), §28 (Gibbs distribution)
- Landau Vol.1 §46 (Liouville theorem — phase volume conservation)
- Landau Vol.10: kinetic theory (non-equilibrium generalization)
