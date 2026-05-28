---
skill_id: knowledge.quantum.schrodinger_equation
type: knowledge
summary_50t: >
  iℏ∂Ψ/∂t = −(ℏ²/2m)∇²Ψ + UΨ. Stationary: −(ℏ²/2m)∇²ψ + Uψ = Eψ.
  Free particle: ψ = A e^{i(p·r−Et)/ℏ}. Continuity: ∂|Ψ|²/∂t + div j = 0.
trigger:
  - solving quantum wave equation
  - energy levels of bound systems
  - time evolution of quantum states
reasoning_role: quantum_dynamics
parent: reasoning.classical_to_quantum_correspondence
retrieval_cost: 1
---

# knowledge.quantum.schrodinger_equation

**Time-dependent**: iℏ ∂Ψ/∂t = ĤΨ,  Ĥ = −(ℏ²/2m)∇² + U(r,t).

**Stationary states** (U≠U(t)): Ψ = ψ(r)e^{−iEt/ℏ},  Ĥψ = Eψ.

**Probability density**: ρ = |Ψ|². Current: j = (iℏ/2m)(Ψ∇Ψ* − Ψ*∇Ψ).
Continuity: ∂ρ/∂t + div j = 0.

**Free particle**: ψ = Ae^{ip·r/ℏ}. E = p²/2m. Continuous spectrum E≥0.
de Broglie: λ = 2πℏ/p. Wave packet: ΔxΔp ≥ ℏ/2.

**Bound states** (E<U(±∞)): discrete spectrum. Harmonic oscillator:
E_n = ℏω(n+½). Coulomb: E_n = −me⁴/(2ℏ²n²).

**Galilean transformation**: Ψ'(r,t) = Ψ(r+Vt,t)·exp[i(mV·r + mV²t/2)/ℏ].

- Landau Vol.3 §17-25
