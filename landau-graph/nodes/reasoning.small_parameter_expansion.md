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
  - knowledge.mechanics.normal_modes
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

## Perturbation Theory: A Cross-Volume Quadruple Bridge

The small-parameter-expansion pattern is the SINGLE most cross-referenced
template in the Landau course. It appears in four volumes with identical
logical structure but different names:

| | Classical (V1) | Quantum (V3) | Statistical (V5) | Many-body (V9) |
|---|---|---|---|---|
| **Bare system** | x₀(t) — free oscillation | ψ^(0), E^(0) — unperturbed | F₀, Z₀ — ideal gas | G₀ — free propagator |
| **Small param** | amplitude a/l | ΔE splitting / E^(0) | V/T (interaction/thermal) | V/g(ε_F) (interaction/Fermi) |
| **1st correction** | x₁(t) — forced oscillation | E^(1) = ⟨ψ^(0)|V|ψ^(0)⟩ | F₁ = ⟨V⟩_0 | Σ — self-energy |
| **Method** | Expand EOM in amplitude | Rayleigh-Schrödinger series | Expand ln Z in V/T | Dyson: G = G₀ + G₀ΣG |
| **Key result** | Nonlinear frequency shift | Energy level shift | Virial expansion | Quasiparticle spectrum |

**The parallel structure**:
1. Identify the bare (solvable) system.
2. Express the full system as bare + λ·(perturbation).
3. Expand in λ: 0th = bare, 1st = average of perturbation, 2nd = fluctuation.
4. The SERIES converges only when λ ≪ 1. Check the condition.

**Key subtlety (Vol.5)**: In thermodynamics, the perturbation parameter
is V/T, which is EXTENSIVE — it grows with system size! The series appears
divergent for macroscopic systems. But ln Z cancels the extensive terms
(see `reasoning.cumulant_generating_function` and `reasoning.thermodynamic_perturbation_theory`). This is a non-trivial cross-volume insight.

## Cross-References

- Landau Vol.1 §21-22 (1D oscillations), §23 (many DOF)
- Quantum: harmonic oscillator is the same eigenvalue problem with ħ corrections
- Field theory: small fluctuations → free field theory (quadratic action)
