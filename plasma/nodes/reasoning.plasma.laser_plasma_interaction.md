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

## Derivation Sketch (from nonlinear optical response → laser-plasma coupling)

Starting from `electrodynamics: reasoning.em.nonlinear_optical_response`
(which establishes χ⁽³⁾ and the general framework of medium nonlinearity),
laser-plasma interaction is the specific case where the nonlinear medium
is a COLLISIONLESS PLASMA — the restoring nonlinearity is the ponderomotive
force, not bound-electron anharmonicity:

1. **From χ⁽³⁾ to ponderomotive force**: in a plasma, the third-order
   nonlinear polarization is mediated by the pondermotive force
   f_p = −(e²/4mω²)∇|E|², which expels electrons from high-intensity
   regions. This produces a density perturbation δn ∝ −|E|², which
   through the linear dielectric function ε(ω)=1−ω_p²/ω² couples back
   to the EM wave. The effective χ⁽³⁾ ~ (ω_p²/ω²)(e/mω²c)²|E|².

2. **Three-wave coupling condition** (parametric instabilities): the
   nonlinear current J_NL = −e δn v_osc drives daughter waves. Energy
   and momentum conservation: ω₀ = ω_1 + ω_2, k₀ = k_1 + k_2. KEY
   NON-OBVIOUS STEP: the decay is RESONANT only when BOTH daughter waves
   satisfy their own linear dispersion relations. This triple intersection
   in (k,ω)-space determines the specific k-matching geometry for SRS
   (backscatter: ω_s≈ω₀−ω_p, k_s≈−k₀+2ω_p/c), SBS (ω_s≈ω₀−k₀ c_s), TPD.

3. **Resonance absorption — the Denisov function**: for p-polarized oblique
   incidence, the laser electric field has a component along the density
   gradient, which resonantly drives an electron plasma wave at n_e=n_c.
   The absorbed fraction is f_abs = (1/2) φ²(τ), where τ = (k₀L)^{1/3} sin θ
   and φ(τ) = 2π^{1/2} |Ai'(−τ)| (the derivative of the Airy function).
   The Denisov function φ²(τ) peaks at τ≈0.8 with f_abs≈0.5 (Kruer §5-6).

4. **Hot electron scaling from Iλ²**: resonance absorption produces
   suprathermal electrons with T_h ≈ α (I₁₆ λ_μm²)^{1/3} (Kruer),
   where I₁₆ is intensity in 10¹⁶ W/cm² and α ∼ 10-100 keV depending
   on the model. At higher intensities, J×B (Brunel) heating dominates:
   T_h ∝ (Iλ²)^{1/2} (ponderomotive scaling). The transition occurs
   when v_osc ∼ v_th.

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

**Resonance absorption — quantitative** (Kruer §5-6):
- Tunneling factor: transmission through the evanescent region between
  turning point (n_e = n_c cos²θ) and critical surface (n_e = n_c).
- Denisov function: absorption fraction f_abs = ½ φ²(τ) with
  τ = (k₀L)^{1/3} sin θ, φ(τ) = 2√π |Ai'(−τ)|.
- Optimal angle: sin θ ≈ 0.8/(k₀L)^{1/3}, giving f_abs ≈ 0.3-0.5.
- Hot electron temperature: T_h ≈ C (Iλ²)^{1/3}, where C ∼ 10-100 keV
  at I ∼ 10¹⁵ W/cm², λ ∼ 1 μm. The (1/3) exponent comes from the balance
  between wave-breaking field and thermal transport (Forslund scaling).

**Brunel (vacuum heating)** (Kruer §5-7):
When v_osc ≡ eE₀/mω₀c exceeds the density scale length, electrons are
pulled into vacuum during one half-cycle and slam back into the overdense
plasma during the next. Ejects electrons with energy ∼ ponderomotive.
Resonant when ω ≈ 2ω_p (parametric coupling to plasma wave).

**J×B heating**: T_h ≈ (1 + a₀²)^{1/2} m_e c² — relativistic regime.
At I ∼ 10¹⁸ W/cm², λ ∼ 1 μm, a₀ ∼ 1, T_h ∼ MeV. Scaling: T_h ∝ √(Iλ²).

**Parametric instabilities** (laser → decay waves):

| Process | Decay | Condition | Threshold | Growth rate |
|---------|-------|-----------|-----------|-------------|
| SRS (Raman) | L→L'+EPW | n_e ≤ n_c/4 | I_th ∝ ν_ei ν_L | γ₀/ω₀ ≈ (v_osc/4c) √(ω_p/ω₀) |
| SBS (Brillouin) | L→L'+IAW | n_e ≤ n_c | I_th ∝ ν_ia | γ₀/ω₀ ≈ (v_osc/4c) √(ω₀ c_s/c² k₀) |
| TPD (two-plasmon) | L→EPW+EPW | n_e ≃ n_c/4 | I_th ∝ ν_ei/T_e | γ₀/ω₀ ≈ (v_osc k₀/4ω₀) √(ω_p/ω₀) |
| Filamentation | L→L+δn | n_e < n_c | Self-focusing | γ ∝ I — ponderomotive/thermal |

**SRS growth rate** (backscatter, homogeneous): γ = (k_epw v_osc/4) √(n_c/n_e − 1)^{−1/2}.
In inhomogeneous plasma, the Rosenbluth gain: G = 2πγ² / (v_g1 v_g2 κ'),
where κ' = d(k₀−k_s−k_epw)/dx is the wavevector mismatch gradient.
Convective threshold: G > π (significant amplification).
Absolute threshold: requires feedback mechanism (e.g., trapped EPW).

**SBS growth rate** (backscatter): γ = (k_iaw v_osc/4) √(ω_pi/ω₀) (n_c/n_e)^{1/4}.
Strongest at high-Z, long scale-length plasmas. IAW Landau damping
provides the main saturation.

**TPD growth rate**: γ_tpd = (k_epw v_osc/4). Threshold is low because
both daughter waves are Langmuir — no ion damping penalty. Saturates
by Langmuir decay instability (LDI): EPW → EPW' + IAW.

**Ponderomotive force**: f_p = −(e²/4mω²)∇|E|² → expels plasma from
high-intensity regions → density profile steepening, channel formation.

**Wakefield acceleration** (Tajima & Dawson 1979, Macchi §5-6):
Laser pulse (τ ∼ τ_p/2) drives plasma wave: E_wake ∼ (n_e/n_c)^{1/2} a₀² E_0.
E_0 = cm ω_p/e ≈ 96√(n_e[cm⁻³]) V/m. For n_e=10¹⁸: E_0∼100 GV/m.

**Wakefield scaling — linear regime** (a₀ ≪ 1):
E_wake [GV/m] ≈ a₀² √(n_e[10¹⁸]/1) × 100.
Energy gain ΔE = e E_wake L_acc ∼ a₀² (n_c/n_e) m_e c² × L_acc ω_p/c.
Dephasing length: L_d = λ_p n_c/n_e ∝ n_e^{−3/2}. Dephasing limits
energy in single stage.

**Bubble/blowout regime** (a₀ > 2): laser pulse expels all electrons → spherical
ion cavity → strong focusing + accelerating fields. Self-injection at bubble
rear → quasi-monoenergetic beams (ΔE/E ∼ 1-10%). Scaling:
E_max[GeV] ≈ 1.7 (P[TW]/100)^{1/3} (n_e/10¹⁸)^{−2/3}.
LWFA: E ∼ 1 GeV over ∼cm at P ∼ 100 TW.
PWFA (proton-driven): E ∼ 50 GeV over ∼m.

**Radiation Pressure Acceleration (RPA)** (Macchi §6):
At a₀ ≫ 1, the laser radiation pressure P_rad = (1+R) I/c can dominate
thermal pressure. Three regimes:

| Regime | Mechanism | Ion energy scaling | Notes |
|--------|-----------|-------------------|-------|
| Hole boring | Laser piston pushes critical surface | v_hb/c = √[(1+R)I/c / 2ρ₀c²] | I ∼ 10²⁰ W/cm² needed |
| Light sail | Ultrathin foil accelerated as whole | E_i ∝ I t_pulse / σ | Requires circular polarization |
| Coulomb explosion | Electrons blown out, ion expansion | E_i ∝ T_e ∝ a₀ m_e c² | Low efficiency, broad spectrum |

**Hole boring velocity**: v_hb = c √(Π/(1+Π)) where Π = I/(ρ₀ c³)
for relativistic, or v_hb ≈ √(I/2ρ₀ c) for nonrelativistic (Wilks scaling).
When v_hb exceeds the sound speed, the piston outruns hydro expansion
→ sharp density profile → enhanced RPA efficiency.

## Edge Cases

- **n_e → 0 (underdense limit)**: laser propagates freely, ε → 1.
  Parametric instabilities vanish (no plasma wave to couple to).
  Wakefield acceleration still works if a laser pulse is present — the
  wake amplitude scales as n_e^{1/2}, so lower density → lower wakefield.
  Use linear plasma theory (ε ≈ 1) with weak ponderomotive drive.
- **n_e ≫ n_c (overdense)**: laser cannot propagate beyond the skin depth
  δ ∼ c/ω_p. Absorption is entirely via collisional or resonance mechanisms
  within the skin layer. For solid-density targets, use the Drude model
  with collisions: ε(ω) = 1 − ω_p²/(ω(ω+iν_ei)) — breaks down when
  ν_ei ≫ ω (evanescent with Ohmic heating only).
- **Relativistic transparency** (n_e > n_c but a₀ ≫ 1): the effective
  plasma frequency is reduced by the relativistic mass increase:
  ω_p → ω_p/√⟨γ⟩, ⟨γ⟩ ≈ √(1+a₀²/2). Laser can propagate when
  a₀ > √(2(n_e/n_c − 1)). Breaks down when pulse is too short (τ < ω_p^{−1}) —
  use PIC simulations; fluid/ponderomotive scaling is insufficient.
- **SRS/SBS convective vs absolute**: in a finite plasma, convective gain
  G = 2πγ²/(v_g1 v_g2 κ') determines if the instability matters.
  For G ∼ 1 the backscatter is negligible; G > 10 → significant pump
  depletion. Absolute SRS (trapped EPW → feedback) requires G ≫ 10 and
  only occurs at n_e ∼ n_c/4 with strong pump. When convective gain is
  low, SRS breaks down — backscatter is below noise; use linear propagation
  with no parametric coupling.

## Cross-References

- Handbook PP-3, Kruer, Gibbon, Macchi §5-6
- electrodynamics: reasoning.em.nonlinear_optical_response (χ⁽³⁾ for plasma;
  parent edge — laser-plasma interaction is the plasma specialization of
  general nonlinear optics; bidirectional: the plasma χ⁽³⁾ computed here
  feeds back to nonlinear optics as an example of medium-driven nonlinearity)
- electrodynamics: knowledge.em.strong_field_electrodynamics (a₀ ≫ 1 regime)
