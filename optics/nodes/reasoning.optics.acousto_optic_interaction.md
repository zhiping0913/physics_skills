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

## Edge Cases

- **Acoustic attenuation**: ∝ f² in crystals. Limits high-frequency operation.
- **Thermal effects**: RF power → heating → index change → beam steering.
- **Walk-off**: acoustic beam diverges → limits interaction length.

## Cross-References

- Yariv §9-10, Iizuka §14
- electrodynamics: reasoning.em.nonlinear_optical_response (same math: χ⁽²⁾ mixing)
