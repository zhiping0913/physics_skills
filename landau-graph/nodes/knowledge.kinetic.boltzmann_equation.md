---
skill_id: knowledge.kinetic.boltzmann_equation
type: knowledge
summary_50t: >
  ∂f/∂t + v·∇f + F·∂f/∂p = St f. St f = ∫ w(f'f₁'−ff₁).
  H = ∫ f ln f d³p, dH/dt ≤ 0. Equilibrium: Maxwell-Boltzmann.
trigger:
  - non-equilibrium gas kinetics
  - transport coefficients (viscosity, heat conduction, diffusion)
  - weakly non-uniform gases
reasoning_role: kinetic_foundation
parent: reasoning.kinetic_equation_closure
retrieval_cost: 1
---

# knowledge.kinetic.boltzmann_equation

**Kinetic equation**: ∂f/∂t + v·∂f/∂r + (F/m)·∂f/∂v = St f.

**Collision integral** (Boltzmann): St f = ∫ w(p,p₁→p',p₁')[f'f₁'−ff₁] d³p₁ d³p' d³p₁'.

**H-theorem**: H = ∫ f ln f d³p d³r. dH/dt ≤ 0.
Equality only at local Maxwell-Boltzmann equilibrium → f₀ ∝ exp(−[m(v−V)²/2]/T).

**Macroscopic equations**: Moments of kinetic equation → continuity, Navier-Stokes, heat equation. Transport coefficients (η, κ, D) emerge from the collision integral.

**Chapman-Enskog**: Systematic expansion in Knudsen number Kn = λ/L ≪ 1.
Zeroth order → Euler equations. First order → Navier-Stokes + Fourier.

- Landau Vol.10 §1-8
