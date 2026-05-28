---
skill_id: reasoning.fluctuation_dissipation_quantum
type: reasoning
summary_50t: >
  Response function χ''(ω) = (1/2ℏ)∫dte^{iωt}⟨[x(t),x(0)]⟩.
  Fluctuation-dissipation theorem: ⟨x²⟩_ω = ℏ coth(ℏω/2T) χ''(ω).
  Classical limit (ℏ→0): ⟨x²⟩_ω = (2T/ω) χ''(ω). Nyquist theorem.
trigger:
  - relating thermal/quantum fluctuations to dissipation
  - noise in quantum systems
  - electromagnetic fluctuations, van der Waals forces
reasoning_role: quantum_noise
parent: reasoning.causality_as_constraint
retrieval_cost: 1
---

# reasoning.fluctuation_dissipation_quantum — Response ↔ Fluctuations (Quantum)

## Core Picture

A system's response to external perturbation (characterized by the
susceptibility χ(ω)) and its spontaneous fluctuations are not independent.
The fluctuation-dissipation theorem (FDT) connects them:

⟨x²⟩_ω = (ℏ/2)coth(ℏω/2T) · χ''(ω)

Classical limit (k_B T ≫ ℏω): ⟨x²⟩_ω = (2T/ω)χ''(ω). This is the
Nyquist theorem for Johnson noise: ⟨V²⟩_ω = 4k_B T R(ω).

## Quantum → Classical Transition

The factor coth(ℏω/2T) interpolates:
- ℏω ≪ T: classical flucutations ∝ T
- ℏω ≫ T: quantum zero-point fluctuations ∝ ℏω/2

## Applications in Vol.9

- **Electromagnetic fluctuations** (§75-82): Photon Green's function in medium.
  Van der Waals and Casimir forces from boundary-modified vacuum fluctuations.
  **Critical subtlety (§77)**: Taking Im ε→0 in infinite medium requires the
  order: infinite size FIRST, then Im ε→0. Arbitrarily small Im ε ultimately
  leads to absorption in infinite medium. The transparent-medium limit depends
  on this specific ordering (pattern: limits do not commute).
- **Equal-time E-B correlation vanishes** (§76): E (T-even) and B (T-odd) →
  cross-correlation odd in t → zero at t=0. ⟨Poynting vector⟩ = 0 in equilibrium.
- **Nyquist theorem** (§78): Elegantly derived from FDT: x=J(t), f=−ℰ,
  α(ω)=iω/Z(ω) → (J²)_ω = (ℏω/|Z|²)R(ω)coth(ℏω/2T). Classical:
  (ℰ²)_ω = 2T R(ω). Universal — independent of the nature of resistance.
- **Hydrodynamic fluctuations** (§86-91): Dynamic form factor S(q,ω) measured
  by inelastic scattering → density-density correlator.

## Connection to Green's Functions

χ(ω) = −(i/ℏ)∫dte^{iωt}⟨[x(t),x(0)]⟩ = retarded Green's function.
The spectral density = Im χ(ω). The FDT gives the symmetrized correlator.

## Cross-References
- Landau Vol.9 §75-91
- Landau Vol.5 §122-123 (classical FDT)
- Landau Vol.8 §77 (Kramers-Kronig — Re ε ↔ Im ε from causality)
