---
skill_id: reasoning.adiabatic_invariance
type: reasoning
summary_50t: >
  When a system parameter λ changes slowly (T|λ̇| ≪ |λ|), the action
  I = (1/2π)∮p dq is conserved to exponential accuracy. This is the
  bridge from classical mechanics to old quantum theory and plasma physics.
trigger:
  - slowly varying system parameter
  - need an approximate conserved quantity
  - T|dλ/dt| ≪ |λ|
reasoning_role: timescale_separation
parent: reasoning.timescale_hierarchy
children:
  - knowledge.mechanics.adiabatic_invariant
  - knowledge.mechanics.action_angle_variables
related:
  - reasoning.separation_of_variables
retrieval_cost: 1
---

# reasoning.adiabatic_invariance — Slow Parameter → Conserved Action

## Core Picture

A system with a slowly changing parameter λ(t) has no exact energy
conservation — it's not closed. But if the change is slow compared to
the system's natural period, a new quantity emerges as (approximately)
conserved: the action I = (1/2π)∮p dq.

The adiabatic invariant is NOT an obvious conserved quantity.
It emerges from AVERAGING the fast oscillatory energy change over
one period of the trajectory with λ held constant. **Crucially, the
averaging is over the FICTITIOUS motion at fixed λ, not the true
motion** — the true orbit doesn't even close, but we average over
the closed orbit of the λ=constant system.

**Key Insight**: I = ∮p dq / 2π is exactly the quantity that becomes
quantized in old quantum theory: I = nℏ (Bohr-Sommerfeld quantization).
The adiabatic invariant is THE bridge from classical mechanics to
quantum mechanics — this is historically how quantization was discovered.

## Algorithm

```
1. Verify slowness: T|λ̇| ≪ |λ|
2. Write dE/dt = (∂H/∂λ)λ̇. This oscillates on the fast timescale.
3. Average over one period of the FICTITIOUS unperturbed motion
   (λ held constant — NOT the true orbit, which doesn't close):
   ⟨dE/dt⟩ = λ̇·⟨∂H/∂λ⟩_period, where the average is over the
   closed orbit of the λ=constant system
4. Convert time integral to phase space integral:
   dt = dq/(∂H/∂p) → ⟨∂H/∂λ⟩ = (∮ ∂H/∂λ dq/(∂H/∂p)) / (∮ dq/(∂H/∂p))
5. Using H(q,p;λ)=E → ∂H/∂λ = −(∂H/∂p)(∂p/∂λ)_E:
   ⟨dE/dt⟩ = −λ̇ (∮ ∂p/∂λ dq) / (∮ ∂p/∂E dq)
6. This is equivalent to: d/dt(∮p dq) = 0
7. I = (1/2π)∮p dq is the adiabatic invariant
```

## Action-Angle Variables

With I as momentum, define conjugate angle w:
  ẇ = dE/dI = ω(I) (constant for fixed λ)
  İ = 0
  Δw = 2π per period (w is the phase)

These are the natural variables for perturbation theory.

## Error Estimate

If λ(t) is analytic, ΔI ∝ exp(−C/|λ̇|) — exponentially small.
Much better than the naive T|λ̇| estimate.

## Key Examples

| System | Adiabatic Invariant |
|--------|-------------------|
| Harmonic osc. with ω(t) | I = E/ω → E ∝ ω |
| Pendulum with lengthening string | I = E/ω (amplitude decreases when string lengthens) |
| Kepler with α(t) | I_r, I_φ → eccentricity fixed, a ∝ 1/α |
| Charged particle in B(t) | μ = mv_⊥²/2B (magnetic moment) |

## Edge Cases

- **Non-integrable systems**: The derivation requires the unperturbed
  motion to be expressible as p = p(q;E,λ) — possible only for INTEGRABLE
  systems (1D bounded, or separable multi-DOF). For non-integrable systems
  (e.g., 3-body problem, chaotic motion), the adiabatic invariant concept
  is not well-defined. Template FAILS.
- **Resonance crossing**: In multi-DOF systems, if frequencies cross during
  λ-change, adiabatic invariance can break.
- **Separatrix crossing**: Near a separatrix, T → ∞ → slowness condition fails.
- **Non-analytic λ(t)**: Error degrades from exponential to power-law.

## Cross-References

- Landau Vol.1 §49-52 (Adiabatic invariants, action-angle, conditionally-periodic motion)
- Old quantum theory: Bohr-Sommerfeld quantization I = nℏ
- Plasma: magnetic moment μ is THE first adiabatic invariant
- Vol.5: thermodynamic adiabatic theorem
