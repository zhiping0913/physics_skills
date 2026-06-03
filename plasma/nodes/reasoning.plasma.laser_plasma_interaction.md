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

## Three Regimes by Iλ² (approximate — depends on Z, T_e, L_n)

```
Iλ² < 10¹⁴ W·μm²/cm²: COLLISIONAL (inverse bremsstrahlung dominant)
10¹⁴ < Iλ² < 10¹⁶: PARAMETRIC INSTABILITIES (SRS, SBS, TPD)
Iλ² > 10¹⁶: PONDEROMOTIVE (profile modification, hole boring)
Iλ² > 10¹⁸: RELATIVISTIC (a₀ = eE/mωc > 1, wakefield)
```

Boundaries are order-of-magnitude. Higher Z or lower T_e extends
collisional regime. Shorter L_n raises parametric thresholds.

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

**Bubble/blowout regime** (a₀>2): laser pulse expels all electrons → spherical
ion cavity → strong focusing + accelerating fields. Self-injection at bubble
rear → quasi-monoenergetic beams (ΔE/E∼1-10%). Scaling: E_max[GeV]≈1.7(P[TW]/100)^{1/3}
(n_e/10¹⁸)^{-2/3}. LWFA: E∼1 GeV over ∼cm at P∼100TW.
PWFA (proton-driven): E∼50 GeV over ∼m.

**Resonance absorption** (oblique p-pol, θ≠0): laser tunnels from n_e=n_c cos²θ
to critical surface. Absorption fraction: f_abs≈½φ²(τ), τ=(k₀L)^{1/3}sinθ.
Optimal angle sinθ≈0.8/(k₀L)^{1/3}. Hot electron temperature scaling:
T_hot≈α(Iλ²)^{1/3} (α depends on model, ∼10-100 keV at I∼10¹⁵ W/cm², λ∼1μm).
Brunel (vacuum heating): v_osc>L_n→electrons pulled into vacuum→return with
energy∼ponderomotive→resonant at ω=2ω_p. J×B heating: T_hot∼(Iλ²)^{1/2}.

**SRS growth rate** (backscatter): γ/ω₀≈(k_epw v_osc/4)√(ω_p/ω₀) where
v_osc=eE₀/mω₀c. Threshold: γ>ν_ei (collisional) or γL_n/c>1 (convective).
SRS saturates by pump depletion or Langmuir wave breaking/collapse.

## Cross-References

- Laser Plasma Handbook (1991), Kruer (1988), Gibbon (2005)
- electrodynamics: reasoning.em.nonlinear_optical_response (χ⁽³⁾ for plasma)
- electrodynamics: knowledge.em.strong_field_electrodynamics (a₀ ≫ 1 regime)
