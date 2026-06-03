---
skill_id: reasoning.optics.acousto_optic_interaction
type: reasoning
summary_50t: >
  Acoustic wave → traveling index grating → Bragg diffraction: 2Λ sin θ_B=λ/n.
  Efficiency η=sin²(πL/λ√(M₂I_a/2)). Deflector: θ∝f_a. Modulator bandwidth
  Δf≈0.35v_s/d. AO tunable filter: λ selected by f_a. Figure of merit M₂=n⁶p²/ρv³.
trigger:
  - designing AO modulators, deflectors, tunable filters
  - frequency shifting laser beams
reasoning_role: acousto_optics
parent: reasoning.em.nonlinear_optical_response
retrieval_cost: 1
sign_convention: >
  Phase matching: k_diff = k_inc + K_sound, ω_diff = ω_inc + Ω_sound (+1 order).
  Frequency upshift (+1 order): photon absorbs acoustic phonon.
  Frequency downshift (−1 order): photon emits acoustic phonon (Stokes process).
  Bragg angle: sin θ_B = λ/(2nΛ) (first order). θ measured inside crystal.
  M₂ = n⁶p²/ρv³ — figure of merit, larger is better (TeO₂: 1200×10⁻¹⁵ s³/kg).
references:
  - electrodynamics: reasoning.em.nonlinear_optical_response (nonlinear wave mixing)
  - plasma: reasoning.plasma.wave_particle_resonance (Bragg = momentum matching)
---

# reasoning.optics.acousto_optic_interaction — Sound → Index Grating → Diffraction

## Core Picture

An acoustic wave in a crystal creates a TRAVELING refractive index grating
via the photoelastic effect: Δn ∝ p·S where p is the photoelastic tensor
and S is the strain. Light incident at the Bragg angle θ_B is diffracted
(Yariv §9-10, Iizuka §14).

## Derivation Sketch

Starting from `electrodynamics: reasoning.em.nonlinear_optical_response`
(χ⁽²⁾ parametric wave mixing: ω₃ = ω₁ + ω₂, k₃ = k₁ + k₂ — a nonlinear
polarization at the sum/difference frequency drives new field components):

1. **Acousto-optic interaction as parametric wave mixing** (consuming parent):
   The acoustic wave modulates the dielectric tensor via the photoelastic
   effect:
   ```
   Δε_{ij} = −ε₀ n⁴ p_{ijkl} S_{kl}
   ```
   where p_{ijkl} is the photoelastic tensor (dimensionless, ~0.1-0.3) and
   S_{kl} is the strain tensor from the acoustic wave. This creates a
   nonlinear polarization P_NL = Δε·E_inc that oscillates at ω_inc ± Ω_sound
   with wavevector k_inc ± K_sound. This IS a χ⁽²⁾ process: two input waves
   (optical + acoustic) produce a third (diffracted optical) via sum/difference
   frequency generation. The parent edge is ACTIVELY consumed: acousto-optic
   interaction is exactly parametric three-wave mixing with one wave being
   an ACOUSTIC phonon instead of an optical field.

2. **Bragg condition as phase matching** (key non-obvious step):
   For efficient energy transfer, the nonlinear polarization wave must
   phase-match to the diffracted optical wave over the interaction length L.
   The condition k_diff = k_inc + K_sound is the MOMENTUM conservation in
   parametric mixing — identical in structure to χ⁽²⁾ phase matching,
   but with the acoustic wavevector K = 2π/Λ ≈ 10⁴−10⁶ m⁻¹ (much smaller
   than optical k ≈ 10⁷ m⁻¹). Geometrically:
   ```
   2Λ sin θ_B = λ/n
   ```
   This is isomorphic to X-ray Bragg diffraction (same equation, different
   physics: here the "crystal planes" are MOVING at speed v_s). The
   traveling nature of the grating Doppler-shifts the diffracted frequency
   by ±Ω_sound.

3. **Bragg vs. Raman-Nath regimes** (Q parameter):
   ```
   Q = 2π λ L / (n Λ²)
   ```
   Q ≫ 1: Bragg regime (thick grating) — single diffraction order. Phase
   matching is selective: only incidence at θ_B produces efficient diffraction.
   Q ≪ 1: Raman-Nath regime (thin grating) — multiple orders, analogous to
   diffraction from a thin phase grating. The transition is smooth; Q ≈ 4π
   is the practical threshold for Bragg operation. Most practical devices
   operate at Q > 10.

4. **Diffraction efficiency from coupled-wave theory** (Kogelnik):
   ```
   η = sin²(πL/λ √(M₂ I_a/2))
   ```
   where M₂ = n⁶p²/(ρv_s³) is the figure of merit. Derivation: solve
   coupled-wave equations for incident and diffracted amplitudes with the
   periodic perturbation Δε(z) = Δε₀ cos(Ωt − Kz). The sin² dependence is
   characteristic of a two-level Rabi oscillation in space — the energy
   oscillates between incident and diffracted beams as they propagate
   through the grating. Maximum efficiency η = 1 at πL/λ √(M₂ I_a/2) = π/2.

## Phonon Picture (Quantum Acousto-Optics — Yariv & Yeh §9-10)

The acousto-optic interaction admits a clean quantum description that
illuminates the frequency shift:

- An acoustic wave of frequency Ω is a coherent state of PHONONS with
  energy ℏΩ and momentum ℏK.
- The +1 order (anti-Stokes): ω_diff = ω_inc + Ω. The incident photon
  ABSORBS an acoustic phonon — energy and momentum conserved:
  ```
  ℏω_diff = ℏω_inc + ℏΩ
  ℏk_diff = ℏk_inc + ℏK
  ```
- The −1 order (Stokes): ω_diff = ω_inc − Ω. The incident photon EMITS
  an acoustic phonon — stimulated phonon emission. The photon loses
  energy to the sound field.
- For N acoustic phonons in the mode, the stimulated emission rate is
  ∝ N (Bose enhancement), so the frequency shift IS quantized: exactly
  ±Ω per photon interaction, not a classical Doppler shift (though the
  classical and quantum pictures agree for the average frequency shift
  in a coherent state).

This quantum picture is essential for understanding:
- **AO frequency shifters (AOFS)** in heterodyne interferometry: the
  frequency shift of exactly f_a (RF drive) ± mHz stability from the
  RF synthesizer.
- **Single-phonon AO** in quantum optomechanics: at the single-phonon
  level, the Stokes/anti-Stokes asymmetry (Stokes is stronger in the
  unresolved-sideband regime) enables laser cooling of acoustic modes.

## Algorithm

```
1. BRAGG CONDITION (thick grating, Q = 2πλL/nΛ² ≫ 1):
   Phase matching: k_diff = k_inc + K_sound
   2Λ sin θ_B = λ/n   (same as X-ray diffraction from crystal planes!)

2. DIFFRACTION EFFICIENCY (Bragg regime):
   η = sin²(πL/λ √(M₂ I_a/2))
   where M₂ = n⁶p²/ρv³ is the acousto-optic figure of merit.
   I_a = acoustic intensity, L = interaction length.

3. RAMAN-NATH REGIME (thin grating, Q ≪ 1):
   Multiple diffraction orders. Intensity: J_m²(Δφ). Δφ=2πLΔn/λ.

4. AO DEFLECTOR: f_a → θ = (λ/nv_s)f_a. N resolvable spots = τ Δf.
   τ = d/v_s (aperture transit time). Bandwidth Δf ≈ 0.35/τ.

5. AO MODULATOR: RF amplitude → η. Rise time τ = d/v_s.
   Bandwidth ≈ 0.35/τ. Digital (on/off) or analog modulation.

6. AO FREQUENCY SHIFTER (AOFS): diffracted beam shifted by ±f_a.
   +1 order: ω_out = ω_in + Ω_sound. Used in heterodyne interferometry.

7. AO TUNABLE FILTER (AOTF): RF f_a selects λ via Bragg condition.
   Spectral resolution: Δλ/λ ∝ Λ/L. RF scan → spectral scan.
```

## Key Materials

| Material | M₂ (10⁻¹⁵ s³/kg) | n | v_s (km/s) | Notes |
|----------|-------------------|---|-----|-------|
| TeO₂ | 1200 | 2.26 | 4.2 (L), 0.62 (S) | Best for deflectors (slow shear) |
| PbMoO₄ | 36 | 2.26 | 3.63 | Good for modulators |
| LiNbO₃ | 7 | 2.20 | 6.57 | Integrated optics |
| Fused silica | 1.5 | 1.46 | 5.96 | Low cost, UV |

## AOPDF / Dazzler (Acousto-Optic Programmable Dispersive Filter)

An important application linking AO to ULTRASHORT PULSE CONTROL (Tournois
1997, Verluise 2000):

A long chirped acoustic pulse (duration ~ tens of μs) creates a spatially
and spectrally varying grating. Different optical wavelengths are diffracted
at different spatial positions along the crystal → different group delays.
By programming the RF waveform (amplitude and phase modulation), the device
acts as an arbitrary spectral amplitude AND phase filter:
```
φ(ω) ∝ RF waveform amplitude and phase at position z(ω)
```
Applications: GDD/TOD compensation in CPA, programmable pulse shaping
(replacing 4-f line with SLM), and CEP control. The Dazzler is a compact
alternative to grating + SLM pulse shapers for moderate bandwidths (< 100 nm).
Bidirectional with `optics: reasoning.optics.dispersion_management_gdd`.

## Edge Cases

- **Acoustic attenuation**: ∝ f² in crystals. Limits high-frequency operation.
  At f_a > 1 GHz in TeO₂, attenuation exceeds 10 dB/cm — switch to thin-film
  ZnO transducers on high-acoustic-Q materials (sapphire, YAG) or use
  surface acoustic waves (SAW) on LiNbO₃ for GHz operation.
- **Thermal effects**: RF power → heating → index change → beam steering.
  Active cooling (water or TEC) is necessary for > 1 W RF. For precision
  deflectors (laser scanning microscopy), thermal drift calibration or
  closed-loop position sensing is essential.
- **Walk-off**: acoustic beam diverges → limits interaction length.
  Use acoustic focusing (curved transducer, cylindrical lens in crystal)
  or anisotropic acousto-optic interaction (TeO₂ slow shear — acoustic
  walk-off is exactly compensated by optical walk-off at the design angle).
- **Multi-frequency operation** (AOD for multi-spot generation): driving
  the transducer with multiple RF frequencies generates multiple diffracted
  beams. Intermodulation products (2f₁−f₂, etc.) appear at ~ (η/N_spots)²
  intensity. Mitigation: operate at η < 50% per beam (linear regime) and
  use pre-distortion of RF drive amplitudes.

## Cross-References

- Yariv §9-10, Iizuka §14
- electrodynamics: reasoning.em.nonlinear_optical_response (same math: χ⁽²⁾ mixing;
  parent edge: Derivation Sketch step 1 shows AO IS parametric three-wave
  mixing with an acoustic phonon — this parent is actively consumed)
- plasma: reasoning.plasma.wave_particle_resonance (Bragg = momentum matching,
  Landau damping = resonant wave-particle interaction analogous to phonon-photon
  energy exchange in AO)
- optics: reasoning.optics.dispersion_management_gdd (AOPDF/Dazzler: AO device
  for arbitrary spectral phase control in CPA. Bidirectional: dispersion_management
  provides the GDD requirements; acousto_optic provides the AOPDF implementation)
