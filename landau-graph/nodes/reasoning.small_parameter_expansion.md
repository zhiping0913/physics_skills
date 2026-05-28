---
skill_id: reasoning.small_parameter_expansion
type: reasoning
summary_50t: >
  Near equilibrium, expand to quadratic order → dynamics reduce to
  linear ODEs with constant coefficients. This is the universal
  entry point to perturbation theory.
trigger:
  - system near stable equilibrium
  - need linearized equations of motion
  - small amplitude oscillations
reasoning_role: perturbation_expansion
parent: reasoning.timescale_hierarchy
children:
  - knowledge.mechanics.small_oscillations_1d
  - knowledge.mechanics.normal_modes
  - knowledge.mechanics.dissipation
related:
  - reasoning.normal_mode_decomposition
retrieval_cost: 1
---

# reasoning.small_parameter_expansion — Small Parameter → Quadratic Approximation

## Core Picture

When a system is near a stable equilibrium (minimum of potential), the
potential can be Taylor-expanded. The constant term is irrelevant (shifts
energy zero), the linear term vanishes at equilibrium, and the quadratic
term dominates. Result: linear ODEs with constant coefficients.

This is NOT just for mechanics. It is the universal first step of almost
every perturbation theory in physics.

## Algorithm

```
1. Identify equilibrium: ∂U/∂q_i = 0, ∂²U/∂q_i∂q_j positive definite
2. Define small displacements: x_i = q_i − q_i0
3. Expand U to second order: U = (1/2) Σ k_ij x_i x_j
4. Expand T to second order at equilibrium: T = (1/2) Σ m_ij ẋ_i ẋ_j
5. Lagrange equations → linear constant-coefficient ODEs:
   Σ m_ij ẍ_j + k_ij x_j = 0
```

## Key Insight

The system can always be diagonalized (see reasoning.normal_mode_decomposition)
→ s independent harmonic oscillators. The frequencies ω_α are the
eigenvalues of m⁻¹k, and they are guaranteed positive (by stability) and real
(by symmetry of k and m).

## Edge Cases

- **Flat direction**: If U has a zero eigenvalue → Goldstone mode,
  quadratic approximation fails → need higher order.
- **Unstable equilibrium**: U is a maximum → imaginary frequencies →
  exponential growth (not oscillation).
- **Large amplitudes**: Quadratic approximation breaks → anharmonic terms
  (see knowledge.mechanics.nonlinear_oscillations).

## Cross-References

- Landau Vol.1 §21-22 (1D oscillations), §23 (many DOF)
- Quantum: harmonic oscillator is the same eigenvalue problem with ħ corrections
- Field theory: small fluctuations → free field theory (quadratic action)
