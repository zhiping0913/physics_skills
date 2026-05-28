---
skill_id: reasoning.periodic_parametric_instability
type: reasoning
summary_50t: >
  When a system parameter oscillates at ~2ω₀/n, parametric resonance
  occurs. Floquet theory: solutions are e^{st}×periodic, with s>0 in
  instability bands near γ = 2ω₀/n.
trigger:
  - periodically varying parameter in an oscillator
  - need to determine stability of a time-dependent system
  - Mathieu-type equation
reasoning_role: instability_analysis
parent: reasoning.variational_principle
children:
  - knowledge.mechanics.parametric_resonance
related:
  - reasoning.small_parameter_expansion
retrieval_cost: 1
---

# reasoning.periodic_parametric_instability — Periodic Driving → Instability Bands

## Core Picture

If the parameters of an oscillator (ω² itself) vary periodically with
frequency γ, the system can become unstable even WITHOUT a driving force.
The equation ẍ + ω²(t)x = 0 with ω(t+T) = ω(t) has solutions of the
form x(t) = μ^(t/T) Π(t) where Π(t+T) = Π(t).

When |μ| > 1, one solution grows exponentially → parametric resonance.

## Algorithm (Floquet Analysis)

```
1. Write equation: ẍ + ω²(t)x = 0, ω(t+T) = ω(t)
2. Two independent solutions: x₁(t+T) = μ₁x₁(t), x₂(t+T) = μ₂x₂(t)
3. Wronskian conservation forces μ₁μ₂ = 1
4. Reality condition: either |μ₁| = |μ₂| = 1 (stable), or μ₁ = 1/μ₂ > 1 (unstable)
5. For weak modulation ω²(t) = ω₀²(1 + h cos γt), h ≪ 1:
   Primary resonance at γ ≈ 2ω₀
   Instability window: |γ − 2ω₀| < hω₀/2
   Growth rate s = (1/2)√[(hω₀/2)² − (γ−2ω₀)²]
6. Higher resonances at γ = 2ω₀/n, width ∝ hⁿ
```

## Key Insight: Why 2ω₀?

The driving modulates the oscillator's natural frequency. The oscillator
"sees" its own motion at ω₀. The parametric drive creates sidebands at
ω₀ ± γ. When γ ≈ 2ω₀, the lower sideband hits ω₀ → resonant feedback.

## Physics of the Instability

At t=0, the oscillator is at x=0, moving right. The frequency suddenly
increases → oscillator is "stiffer" → it turns around faster, gaining
energy. After half a period, the frequency decreases → oscillator is
"softer" → overshoots. Net energy gain per cycle. This is fundamentally
different from forced resonance (where energy input is from external driving).

## Edge Cases

- **Effect of damping**: Friction narrows the instability window.
  Condition: s > λ (growth exceeds damping).
- **Large h**: Multiple instability bands overlap, analysis needs Mathieu functions.
- **Non-periodic variation**: Floquet theory fails → need adiabatic theory or numerics.

## Cross-References

- Landau Vol.1 §27 (Parametric resonance)
- Mathieu equation: standard form d²x/dτ² + (a − 2q cos 2τ)x = 0
- Plasma: parametric instabilities in laser-plasma interaction (stimulated Raman, Brillouin)
