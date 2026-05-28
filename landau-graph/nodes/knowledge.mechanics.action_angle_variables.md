---
skill_id: knowledge.mechanics.action_angle_variables
type: knowledge
summary_50t: >
  (w,I) are canonical variables: ẇ = ω(I) = const, İ = 0 for closed system.
  w is the phase (Δw = 2π per period). Foundation of perturbation theory.
trigger:
  - integrable system → construct action-angle variables
  - need variables that are constant in the unperturbed system
reasoning_role: canonical_variables_for_integrable_systems
parent: knowledge.mechanics.adiabatic_invariant
retrieval_cost: 1
---

# knowledge.mechanics.action_angle_variables

**Definition**:
```
I = (1/2π)∮p dq          action (momentum-like)
w = ∂S₀(q,I)/∂I          angle (coordinate-like)
```

**Equations of motion**:
```
İ = 0                    action constant for closed system
ẇ = dE/dI = ω(I)         angle advances linearly
Δw = 2π per period        periodicity in w
```

**For multi-DOF separable systems**: s pairs (wᵢ, Iᵢ).
Equation of H-J: S₀ = Σ ∫pᵢ(qᵢ;α₁,...,α_s)dqᵢ.
Then Iᵢ(α) → E(I₁,...,I_s), ωᵢ = ∂E/∂Iᵢ.

**Degeneracy**: When ωᵢ commensurate → fewer independent frequencies.
Kepler: ω_r = ω_φ → orbit closes after one period.

**For slowly varying λ(t)**: w, I equations get corrections:
İᵢ = −(∂Λ/∂wᵢ)λ̇,  ẇᵢ = ωᵢ + (∂Λ/∂Iᵢ)λ̇
where Λ = (∂S₀/∂λ)_{q,I}.

**Application**: Starting point for Hamiltonian perturbation theory
and KAM theory. Foundation of old quantum theory (I = nℏ).

- Landau Vol.1 §50, §52
