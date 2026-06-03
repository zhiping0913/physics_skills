---
skill_id: knowledge.optics.stimulated_scattering_engineering
type: knowledge
summary_50t: >
  SBS: acoustic phonon, g_B∼5×10⁻¹¹m/W, Δν∼10-100MHz, P_th≈21A_eff/g_B L_eff.
  Phase conjugation. SRS: optical phonon, g_R∼10⁻¹³m/W, shift∼13THz (silica).
  Cascaded Raman→supercontinuum. Damage: diel breakdown∼10-100GW/cm², self-focus
  P>P_cr, multiphoton ionization. **Differs from plasma SBS/SRS** (no ion waves here).
trigger: fiber laser design, high-power nonlinear mitigation, damage threshold
reasoning_role: stim_scattering
parent: reasoning.em.nonlinear_optical_response
retrieval_cost: 1
references:
  - electrodynamics: reasoning.em.nonlinear_optical_response
  - plasma: knowledge.plasma.laser_plasma_processes (SBS/SRS in plasma — different physics!)
---

# knowledge.optics.stimulated_scattering_engineering

**SBS** (Boyd §9): Electrostriction → acoustic phonon. Gain g_B∼5×10⁻¹¹ m/W (silica).
Lorentzian: g_B(Ω)=g_B (Γ_B/2)²/[(Ω−Ω_B)²+(Γ_B/2)²]. Γ_B/2π∼10-100 MHz.
Threshold: P_th≈21 A_eff/(g_B L_eff). SBS reflected wave is Stokes-shifted by
ν_B=2nv_s/λ∼11GHz (silica at 1.55μm). Phase conjugation: SBS reflected wave
reverses incident wavefront — beam cleanup through aberrated media.

**SRS** (Boyd §10): Optical phonon → molecular vibration. g_R∼10⁻¹³ m/W (silica),
broadband (Δν∼THz). Stokes shift ∼13 THz. Raman amplifier: CW pump + signal →
signal gain. Cascaded Raman: each Stokes order pumps next → broad spectrum.
Raman fiber laser: FBG pair + Raman gain → wavelength-flexible.

**SBS vs plasma SBS**: Plasma SBS involves ion acoustic waves (ω_iaw, k_iaw),
ponderomotive coupling, and depends on n_e/n_c. FIBER SBS involves acoustic
phonons (Ω_B, K_B), electrostriction, and depends on material M₂ figure.
Completely different physical mechanisms — only the name and 3-wave structure
are shared.

**Damage mechanisms** (Boyd §12):
Dielectric breakdown: multiphoton ionization (ω_gap∼9eV for SiO₂ → n∼3 photons
at 355nm). Rate W_MPI∝I^n. Avalanche: seed e⁻ accelerated → impact ionization →
exponential growth. Combined: W(I)=W_MPI+ W_av. Damage fluence F_th∼10-100 J/cm²
for ns, ∼1 J/cm² for ps, ∼0.1 J/cm² for fs pulses.
Self-focusing damage: P>P_cr=αλ²/(4πn₀n₂), α≈1.86 for Gaussian.
Thermal: absorption → heating → stress → fracture.

- Boyd §9-10, §12
