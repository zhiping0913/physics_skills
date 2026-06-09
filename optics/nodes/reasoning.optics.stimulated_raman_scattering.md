---
skill_id: reasoning.optics.stimulated_raman_scattering
type: reasoning
summary_50t: >
  SRS: pump ω_p → Stokes ω_S + material excitation Ω=ω_p−ω_S. Same 3-wave
  structure bridges fiber (molecular vibration) and plasma (Langmuir wave).
  Raman χ⁽³⁾ from driven Lorentzian oscillator → g_R from Im[χ⁽³⁾] → exponential
  amplifier growth. Threshold: g_R I_p L ≳ 25.
trigger:
  - Raman amplifier design (fiber, gas, plasma)
  - predicting Stokes shift from material resonance
  - SRS threshold and gain in high-power systems
  - understanding plasma↔fiber SRS analogy
reasoning_role: raman_scattering
parent: reasoning.em.nonlinear_optical_response
retrieval_cost: 1
references:
  - electrodynamics: reasoning.em.nonlinear_optical_response
  - plasma: reasoning.lp.laser_propagation_plasma
  - optics: knowledge.optics.stimulated_scattering_engineering
  - optics: reasoning.optics.pulse_propagation_nlse
---

# reasoning.optics.stimulated_raman_scattering — Pump→Stokes + Material Excitation

## Core Picture

SRS: pump photon (ω_p) → Stokes photon (ω_S) + material excitation (Ω = ω_p − ω_S).
The material excitation can be MOLECULAR VIBRATION (fiber, Raman-active medium),
LANGMUIR WAVE (plasma), or ACOUSTIC PHONON (SBS). Same 3-wave structure in all
cases — only the driven oscillator changes.

```
FIBER SRS:   ω_p  →  ω_S (Stokes)  +  Ω_R (Si-O-Si stretch, ~13.2 THz)
PLASMA SRS:  ω_p  →  ω_S (scattered EM) + ω_pe (Langmuir wave)
FIBER SBS:   ω_p  →  ω_S (Stokes)  +  Ω_B (acoustic phonon, ~11 GHz)
```

This node is the PLASMA↔FIBER ANALOGY BRIDGE — the derivation and algorithm
work identically for both; only the oscillator parameters differ.

## Derivation Sketch

From parent `reasoning.em.nonlinear_optical_response` χ⁽³⁾ framework: the Raman
nonlinearity arises from a DRIVEN OSCILLATOR response.

1. **Material oscillator**: normal mode coordinate q with frequency Ω_R, damping
   Γ, effective mass m. Driven by optical force F ∝ (∂α/∂q) E_p E_S* at the
   beat frequency Ω = ω_p − ω_S. The driving arises from the optical polarizability
   modulation as nuclei move — the same physics as spontaneous Raman but coherent.

2. **Equation of motion**:
   ```
   q̈ + Γ q̇ + Ω_R² q = (1/m)(∂α/∂q) E_p · E_S*
   ```
   Steady-state solution (harmonic drive at Ω): q(Ω) ∝ 1 / (Ω_R² − Ω² − iΩ Γ),
   a Lorentzian centered at Ω_R with FWHM = Γ.

3. **Nonlinear polarization**: the oscillating coordinate q modulates the linear
   polarizability → nonlinear polarization at Stokes frequency:
   ```
   P_NL(ω_S) = ε₀ N (∂α/∂q) q E_p
   ```
   where N is the number density of oscillators. Identifying P_NL = ε₀ χ⁽³⁾_R |E_p|² E_S:
   ```
   χ⁽³⁾_R(Ω) = [N (∂α/∂q)² / (2 m ε₀)] · 1 / (Ω_R² − Ω² − i Ω Γ)
   ```

4. **Raman gain**: the Stokes intensity grows as dI_S/dz = g_R I_p I_S, with
   ```
   g_R = (3 ω_S / n_p n_S ε₀ c²) Im[χ⁽³⁾_R(Ω_R)]
   ```
   At resonance (Ω = Ω_R): Im[χ⁽³⁾_R] = [N (∂α/∂q)²] / (2 m ε₀ Ω_R Γ).
   The gain is linear in pump intensity and proportional to (∂α/∂q)² / Γ.

5. **Amplifier growth** (undepleted pump approximation, I_p ≈ const):
   ```
   I_S(L) = I_S(0) exp(g_R I_p L)
   ```
   Significant conversion when g_R I_p L ≳ 25–30 (≈ exp(25) ∼ 10¹⁰ gain).

6. **Manley-Rowe** (photon flux conservation in lossless medium):
   ```
   I_p/ω_p + I_S/ω_S = const
   ```
   Each pump photon destroyed creates one Stokes photon and one material quantum.

## Algorithm (same for all Raman variants)

```
1. IDENTIFY material excitation frequency Ω_R and equation-of-motion parameters:
   - Fiber: Ω_R/(2π) ≈ 13.2 THz, Γ/(2π) ≈ 7.5 THz (silica)
   - Plasma: Ω_R = ω_pe = √(n_e e² / ε₀ m_e)
   - SBS: Ω_B = 2 n v_s / λ

2. COMPUTE Raman χ⁽³⁾_R from Lorentzian oscillator response:
   χ⁽³⁾_R(Ω) = (constant) / (Ω_R² − Ω² − i Ω Γ)

3. RAMAN GAIN from imaginary part at resonance:
   g_R = (3 ω_S / n_p n_S ε₀ c²) Im[χ⁽³⁾_R(Ω_R)]

4. UNDEPLETED-PUMP GROWTH:
   I_S(L) = I_S(0) exp(g_R I_p L)

5. THRESHOLD: significant conversion when g_R I_p L ≳ 25–30
```

## Fiber SRS — Concrete Parameters

- **Fused silica**: Ω_R/(2π) ≈ 13.2 THz (Si-O-Si stretching mode),
  Γ/(2π) ≈ 7.5 THz → Raman gain bandwidth ~5 THz (broad, amorphous).
- **Peak gain**: g_R ≈ 1×10⁻¹³ m/W at 1.55 μm (Boyd §10, Agrawal §8).
- **SMF-28 amplifier**: L_eff ≈ 20 km (limited by fiber loss α), A_eff ≈ 80 μm².
  Threshold power P_th = 16 A_eff / (g_R L_eff) ≈ 0.6–1.0 W.
- **Polarization dependence**: g_R(∥) ≫ g_R(⊥) — Raman gain in fiber is strongly
  polarization-sensitive. Use polarization scrambling or PM fiber.
- **Gain spectrum**: silica Raman gain is broad (~40 THz total span) with peak
  at 13.2 THz shift. Multiple peaks from different Si-O modes.

## Plasma SRS — Sister Phenomenon (analogous structure)

- **Material excitation**: LANGMUIR WAVE (electron plasma oscillation) at
  Ω_R = ω_pe = √(n_e e² / (ε₀ m_e)).
- **Driving force**: ponderomotive potential ∇(E_p · E_S*) pushes electrons →
  density perturbation δn/n₀. Replaces (∂α/∂q) with ponderomotive coupling.
- **Same coupled 3-wave structure**: the daughter Langmuir wave satisfies its
  own dispersion ω_epw² = ω_pe² + 3 k² v_th² (Bohm-Gross). The triple intersection
  (ω_p = ω_S + ω_epw, k_p = k_S + k_epw) determines matching conditions.
- **Growth rate** (homogeneous plasma, backscatter):
  γ₀/ω₀ ≈ (v_osc/4c) √(ω_pe/ω₀), where v_osc = eE₀/(m ω₀).
- **Gain in inhomogeneous plasma** (Rosenbluth): G = 2πγ₀² / (v_g1 v_g2 κ′),
  κ′ = d(k₀ − k_S − k_epw)/dx. Convective threshold: G > π.
- **Frequency matching constraint**: plasma SRS requires n_e ≤ n_c/4
  (otherwise ω_S < ω_pe and Stokes is below cutoff).
- Cross-ref: `laser-plasma: reasoning.lp.parametric_instabilities_lpi`
  (SRS/SBS/TPD growth rates, convective vs absolute thresholds).
- **Key difference**: plasma SRS has NO material damage threshold (no solid
  lattice); fiber SRS is limited by glass damage (~1 GW/cm²). Plasma SRS
  saturates by Langmuir wave-breaking or pump depletion.

## SBS — Sister Phenomenon (same template)

Same 3-wave structure with ACOUSTIC PHONON (Ω_B ~ 11 GHz in silica at 1.55 μm,
ion-acoustic wave in plasma). Electrostrictive driving replaces polarizability
modulation: electrostriction → density grating → refractive index grating →
Bragg scattering. Cross-ref: `knowledge.optics.stimulated_scattering_engineering`.

## Edge Cases

- **Transient SRS** (pulse duration τ_p < T₂ = 1/Γ): the steady-state Lorentzian
  response fails. Time-domain model needed — the phonon wave builds up during the
  pulse. Gain ∝ √(Γ τ_p) rather than 1/Γ. Use coupled time-domain equations.
- **Cascaded Raman**: first Stokes becomes pump for second Stokes → multi-order
  frequency comb. Each order shifted by Ω_R. Important for supercontinuum and
  Raman fiber lasers.
- **Raman-induced self-frequency shift (SSFS)**: soliton intrapulse Raman
  scattering in anomalous dispersion fiber. The soliton spectrum continuously
  redshifts (Δω ∝ −τ⁻⁴). Cross-ref: `reasoning.optics.pulse_propagation_nlse`
  (intrapulse Raman term T_R in generalized NLSE).
- **Anti-Stokes generation**: ω_AS = ω_p + Ω_R is also phase-matchable via
  four-wave mixing (CARS geometry). Requires Δk = 2k_p − k_S − k_AS ≈ 0.
  Weaker than Stokes in fiber due to phase matching, but important for
  coherent anti-Stokes Raman spectroscopy (CARS) and plasma SRS.
- **Pump depletion**: undepleted-pump approximation fails at high conversion
  (>10%). Full coupled equations:
  dI_p/dz = −(ω_p/ω_S) g_R I_p I_S, dI_S/dz = +g_R I_p I_S.

## Cross-References

- Boyd §10 (SRS theory, oscillator model), Agrawal §8 (fiber Raman amplifiers)
- electrodynamics: reasoning.em.nonlinear_optical_response (parent: χ⁽³⁾ framework;
  Derivation Sketch step 3 builds directly on the parent's χ⁽³⁾ → P_NL formalism)
- plasma: reasoning.lp.laser_propagation_plasma (plasma SRS — same 3-wave
  structure, different oscillator; this node is the plasma↔fiber analogy bridge)
- optics: knowledge.optics.stimulated_scattering_engineering (fiber SRS/SBS
  engineering values, threshold formulas, damage limits)
- optics: reasoning.optics.pulse_propagation_nlse (Raman shift term T_R in
  generalized NLSE; intrapulse Raman → SSFS)
