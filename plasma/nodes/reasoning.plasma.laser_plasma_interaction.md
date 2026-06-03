---
skill_id: reasoning.plasma.laser_plasma_interaction
type: reasoning
summary_50t: >
  Laser incident on plasma → critical surface (n_e=n_c). Three regimes by Iλ²:
  collisional (inverse bremsstrahlung), parametric (SRS/SBS/TPD), relativistic
  (ponderomotive, wakefield). Resonance absorption at oblique p-polarized.
  Thresholds, growth rates, saturation mechanisms.
trigger:
  - laser propagating into plasma, need to compute absorption/reflection
  - parametric instability thresholds and growth rates
  - laser-driven particle acceleration
reasoning_role: laser_plasma
parent: reasoning.em.nonlinear_optical_response
retrieval_cost: 1
references:
  - electrodynamics: reasoning.em.nonlinear_optical_response
  - electrodynamics: knowledge.em.strong_field_electrodynamics
---

# reasoning.plasma.laser_plasma_interaction — EM Wave → Plasma Response

## Core Picture

Laser light incident on plasma is reflected at the CRITICAL SURFACE where
n_e = n_c = ε₀ m_e ω²/e². Below n_c, the laser propagates (ω > ω_p).
Above n_c, it is evanescent. Energy is deposited via:

## Three Regimes by Iλ² (Laser Plasma Handbook, Kruer)

```
Iλ² < 10¹⁴ W·μm²/cm²: COLLISIONAL (inverse bremsstrahlung)
10¹⁴ < Iλ² < 10¹⁶: PARAMETRIC INSTABILITIES (SRS, SBS, TPD)
Iλ² > 10¹⁶: PONDEROMOTIVE (profile modification, hole boring)
Iλ² > 10¹⁸: RELATIVISTIC (a₀ = eE/mωc > 1, wakefield)
```

## Key Processes

**Inverse bremsstrahlung** (collisional absorption):
α_IB ∝ Z n_e² lnΛ / T_e^{3/2} √(1−n_e/n_c). Dominant at low I, high Z.

**Resonance absorption** (oblique p-polarized, θ ≠ 0):
Laser tunnels from reflection point (n_e=n_c cos²θ) to critical surface.
Resonant excitation of plasma wave → hot electrons.

**Parametric instabilities** (laser → decay waves):

| Process | Decay | Condition | Threshold |
|---------|-------|-----------|-----------|
| SRS (Raman) | L→L'+EPW | n_e ≤ n_c/4 | I_th ∝ ν_ei ν_L |
| SBS (Brillouin) | L→L'+IAW | n_e ≤ n_c | I_th ∝ ν_ia |
| TPD (two-plasmon) | L→EPW+EPW | n_e ≃ n_c/4 | I_th ∝ ν_ei/T_e |
| Filamentation | L→L+δn | n_e < n_c | Self-focusing |

**Ponderomotive force**: f_p = −(e²/4mω²)∇|E|² → expels plasma from
high-intensity regions → density profile steepening, channel formation.

**Wakefield acceleration** (Tajima & Dawson 1979):
Laser pulse (τ ∼ τ_p/2) drives plasma wave: E_wake ∼ (n_e/n_c)^{1/2} a₀² E_0.
E_0 = cm ω_p/e ≈ 96√(n_e[cm⁻³]) V/m. For n_e=10¹⁸: E_0∼100 GV/m.

## Cross-References

- Laser Plasma Handbook (1991), Kruer (1988), Gibbon (2005)
- electrodynamics: reasoning.em.nonlinear_optical_response (χ⁽³⁾ for plasma)
- electrodynamics: knowledge.em.strong_field_electrodynamics (a₀ ≫ 1 regime)
