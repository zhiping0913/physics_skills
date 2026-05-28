---
skill_id: reasoning.collision_integral_construction
type: reasoning
summary_50t: >
  St f = ∫ w(f'f₁' − ff₁). From microscopic cross-section to macroscopic transport.
  For Coulomb: Landau collision integral (Fokker-Planck form).
  For neutral gas: Boltzmann collision integral. For quantum: Uehling-Uhlenbeck.
trigger:
  - need collision term for kinetic equation
  - Coulomb collisions in plasma
  - computing relaxation rates, transport coefficients
reasoning_role: collision_operator
parent: reasoning.kinetic_equation_closure
children:
  - knowledge.kinetic.landau_collision_integral
retrieval_cost: 1
---

# reasoning.collision_integral_construction — Microscopic Cross-Section → Collision Operator

## Core Picture

The collision integral St f accounts for how binary collisions change f.
For classical point particles: St f = ∫ w(p,p₁→p',p₁')[f'f₁'−ff₁].

Key structure: gain term (f'f₁') minus loss term (ff₁).
The transition probability w encodes the microscopic cross-section:
w d³p' d³p₁' = |v−v₁| dσ for scattering into (p',p₁').

## Landau Collision Integral (Plasma, §41)

For Coulomb collisions (small-angle scattering dominates):
St f = −∂s_α/∂p_α, where s is the particle flux in momentum space.
s_α = Σ ∫ B_{αβ}(f ∂f₁/∂p₁β − f₁ ∂f/∂p_β) d³p₁
B_{αβ} = (2πe⁴L/2)(u²δ_{αβ} − u_αu_β)/u³, u = v−v₁, L = Coulomb logarithm.

This is a Fokker-Planck form — collisions act as diffusion + drag in momentum space.

## Relaxation Times

Electron-electron: τ_ee ~ m^{1/2}T_e^{3/2}/ne⁴L.
Electron-ion: τ_ei ~ M^{1/2}T_e^{3/2}/nZ²e⁴L.
τ_ei/τ_ee ~ (M/m)^{1/2} ≫ 1 → electrons thermalize among themselves first,
then slowly with ions.

## H-Theorem

dH/dt ≤ 0 for any distribution, with H = ∫ f ln f d³p.
Equality only at equilibrium (Maxwell-Boltzmann).
This proves the irreversible approach to equilibrium from purely
reversible microscopic dynamics — with the Stosszahlansatz (molecular chaos).

## Cross-References
- Landau Vol.10 §3 (Boltzmann integral), §41 (Landau collision integral)
- Landau Vol.5 §8 (law of entropy increase)
