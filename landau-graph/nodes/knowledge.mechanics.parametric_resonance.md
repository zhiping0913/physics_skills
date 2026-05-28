---
skill_id: knowledge.mechanics.parametric_resonance
type: knowledge
summary_50t: >
  ω² = ω₀²(1+h cos γt) with h≪1. Parametric instability when
  γ ≈ 2ω₀/n in bands of width ∝ hⁿ. Growth rate s = ½√[(hω₀/2)²−(γ−2ω₀)²].
trigger:
  - Mathieu equation
  - periodically modulated oscillator parameter
reasoning_role: instability_condition
parent: reasoning.periodic_parametric_instability
retrieval_cost: 1
---

# knowledge.mechanics.parametric_resonance

**Key equation**: ẍ + ω₀²[1+h cos(2ω₀+ε)t]x = 0

**Floquet solution**: x(t) = e^{st} × periodic,  s² = ¼[(hω₀/2)² − ε²]

**Primary instability**: |ε| < hω₀/2 around γ = 2ω₀.
**Higher resonances**: at γ = 2ω₀/n, width ∝ hⁿ.

**With friction**: threshold: s = λ (damping rate)
→ narrows instability window.

- Landau Vol.1 §27
