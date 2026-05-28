---
skill_id: knowledge.mechanics.adiabatic_invariant
type: knowledge
summary_50t: >
  I = (1/2π)∮p dq. Conserved when λ̇ ≪ ω. Phase-space area is invariant.
  Harmonic oscillator: I = E/ω. Kepler: I_φ = M, I_r = −M+α√(m/2|E|).
trigger:
  - slowly varying parameter λ(t) in bounded system
  - need conserved quantity when energy is not conserved
reasoning_role: adiabatic_invariant
parent: reasoning.adiabatic_invariance
children:
  - knowledge.mechanics.action_angle_variables
retrieval_cost: 1
---

# knowledge.mechanics.adiabatic_invariant

**Definition**: I = (1/2π)∮p dq, integral over one period of the orbit
with λ held constant. I(E,λ).  dI/dt averaged = 0.

**Geometric meaning**: I = (1/2π) × (area enclosed by phase trajectory).
For 1D: I = (1/2π)∬dp dq.

**Key results**:
```
∂I/∂E = T/2π (period-energy relation)
∂E/∂I = ω   (frequency as derivative of energy)
```

**Examples**:
- Harmonic osc. ω(t): I = E/ω → E ∝ ω, amplitude ∝ 1/√ω
- Kepler α(t): I_r, I_φ conserved → eccentricity fixed, a ∝ 1/α
- Charged particle B(t): μ = mv_⊥²/2B (magnetic moment)

**Error**: ΔI ∝ exp(−C/|λ̇|) for analytic λ(t).

- Landau Vol.1 §49
