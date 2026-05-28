---
skill_id: knowledge.qed.dirac_equation
type: knowledge
summary_50t: >
  (iγ^μ∂_μ − m)ψ = 0. γ-matrices: {γ^μ,γ^ν}=2g^{μν}. Bispinor ψ.
  Free solutions: u(p)e^{−ipx}, v(p)e^{+ipx}. Positron = −E solution.
  Spin: S^z = (ℏ/2)diag(σ_z,σ_z). g-factor = 2 emerges naturally.
trigger:
  - relativistic electron dynamics
  - spin, magnetic moment
  - particle-antiparticle pair creation
reasoning_role: relativistic_wave_equation
parent: reasoning.dirac_equation_antiparticles
retrieval_cost: 1
---

# knowledge.qed.dirac_equation

**Equation**: (iγ^μ∂_μ − m)ψ = 0. In standard representation:
γ⁰ = diag(1,1,−1,−1), γ = antidiag(σ,−σ).

**Bispinor**: ψ = (ξ, η)^T. In rest frame (p=0): ξ = η (positive E),
ξ = −η (negative E). Two independent spin states for each.

**Plane waves**: ψ = u(p,s)e^{−ipx} (electron), ψ = v(p,s)e^{+ipx} (positron).
u and v satisfy (γ^μp_μ − m)u = 0, (γ^μp_μ + m)v = 0.

**Current**: j^μ = ψ̄γ^μψ, ψ̄ = ψ†γ⁰. Conserved: ∂_μ j^μ = 0.

**Non-relativistic limit**: ψ ≈ (φ, (σ·p/2m)φ)^T → Pauli equation:
iℏ∂φ/∂t = [p²/2m − (e/2mc)σ·B] φ. The g-factor = 2 emerges from Dirac
equation — NOT from experiment. This was Dirac's great triumph.

**Charge conjugation**: ψ → ψ_c = iγ²ψ*. Electron ↔ positron.

- Landau Vol.4 §20-28
