---
skill_id: knowledge.em.strong_field_electrodynamics
type: knowledge
summary_50t: >
  Schwinger limit E_cr=m²c³/eℏ≈1.3×10¹⁶V/cm, I_cr≈4.6×10²⁹W/cm².
  Nonlinear Compton: multi-photon absorption → high harmonics.
  Pair production: γ+nγ_L→e⁺e⁻ (Breit-Wheeler), vacuum → e⁺e⁻ (Schwinger).
  Radiation reaction: Landau-Lifshitz equation, classical η=γE/E_cr.
trigger:
  - laser intensity approaching relativistic/quantum regime
  - pair production, vacuum polarization in strong fields
reasoning_role: strong_field_knowledge
parent: reasoning.em.nonlinear_optical_response
retrieval_cost: 1
---

# knowledge.em.strong_field_electrodynamics

**Schwinger (critical) field**: E_cr = m²c³/eℏ ≈ 1.3×10¹⁶ V/cm.
Corresponding intensity: I_cr = cE_cr²/8π ≈ 4.6×10²⁹ W/cm².
At E∼E_cr, vacuum becomes unstable to spontaneous e⁺e⁻ pair production.

## Classical Strong-Field Regime (a₀ ≫ 1, χ ≪ 1)

**Normalized vector potential**: a₀ = eE/(mωc). a₀ ≫ 1 → relativistic electron
motion. For λ=1μm, I=10¹⁸ W/cm² → a₀≈1. Currently achieved: a₀∼10²−10³.

**Nonlinear Thomson/Compton scattering** (Avetissian §2, §6):
Electron in strong plane wave executes figure-8 motion. Radiation spectrum:
harmonics of ω_L with relativistic Doppler shift → ω_n = nω_L/(1−β cos θ + ...).
High harmonics from nonlinear trajectory, not quantum effects.

**Radiation reaction** (Landau-Lifshitz equation):
m dU^μ/dτ = (e/c)F^{μν}U_ν + (2e³/3mc³)[(e/m)F^{μα}F_{αν}U^ν + ...].
RR force ∼ (2e³/3mc³) γ²(F²). Quantum parameter: χ = γE/E_cr.
When χ∼1, quantum RR dominates (stochastic photon emission).

## Quantum Strong-Field Regime (χ ≳ 1)

**Nonlinear Breit-Wheeler**: γ + n·γ_L → e⁺e⁻ (pair creation from photon +
laser photons). Threshold: n·ℏω_L ≥ 2mc². Rate ∝ exp(−8/3χ) for χ≪1.

**Schwinger mechanism**: Vacuum spontaneously decays to e⁺e⁻ pairs in static
electric field E. Rate per unit volume: w ∝ exp(−πE_cr/E) for E≪E_cr.
Not yet observed (requires E∼E_cr, I∼10²⁹ W/cm²).

**Vacuum polarization** (Euler-Heisenberg):
Effective Lagrangian: L_eff = −F²/4 + (α²/90m⁴)[(F_{μν}F^{μν})² + 7(F_{μν}F̃^{μν})²].
Vacuum behaves as nonlinear medium: n_⊥≠n_∥ (vacuum birefringence).
Probed by: PVLAS experiment, upcoming LUXE at DESY, SEL at SLAC.

**Nonlinear Cherenkov** (Avetissian §3):
Electron in dielectric + strong laser: Cherenkov condition modified by
laser-induced effective refractive index. Resonant enhancement of radiation.

- Avetissian §2, §6, §10; Landau Vol.4 §129-130 (radiative corrections)
