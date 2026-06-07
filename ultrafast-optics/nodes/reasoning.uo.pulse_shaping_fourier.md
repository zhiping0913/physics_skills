---
skill_id: reasoning.uo.pulse_shaping_fourier
type: reasoning
summary_50t: >
  4f-shaper: grating→lens→SLM→lens→grating. Fourier plane at SLM:
  manipulate E(ω) via amplitude mask M(ω) and phase mask φ(ω).
  Output: a_out(t) = F⁻¹{M(ω)e^{iφ(ω)} F{a_in(t)}}. Liquid crystal
  SLM (pixelated 640/1280 pixels), AOM (acousto-optic, continuous).
  MIIPS: adaptive phase scan → self-calibrating compression.
  Applications: arbitrary waveform generation, coherent control.
trigger:
  - designing a pulse shaper for femtosecond waveform synthesis
  - computing the temporal output of a given spectral mask
  - implementing adaptive pulse compression via MIIPS
reasoning_role: fourier_pulse_shaper
parent: reasoning.uo.pulse_propagation_linear
retrieval_cost: 1
sign_convention: >
  4f geometry: input grating → lens (f) → SLM at Fourier plane → lens (f) → output grating.
  Spectral resolution: δλ = λ² d cos θ_in / (f N_g) where N_g = lines illuminated.
  SLM pixel crosstalk limits fidelity. AOM: RF waveform → acoustic grating → diffracted
  spectrum shaped.
references:
  - ultrafast-optics: reasoning.uo.pulse_propagation_linear (pulse representation)
---

# reasoning.uo.pulse_shaping_fourier — 4f-Shaper → E(ω) Masks → a_out(t)

## Core Picture

A 4f Fourier pulse shaper spatially disperses the pulse spectrum onto a
mask plane where each wavelength component can be independently amplitude-
and phase-modulated. Because the time-domain pulse is the Fourier transform
of the shaped spectrum, arbitrary temporal waveforms can be synthesized.
This is the optical analog of a waveform generator in electronics — the
foundation for coherent control, MIIPS compression, and femtosecond
waveform engineering (Weiner §8, Dantus §2-3).

## Derivation Sketch

### 1. 4f-shaper operation (Weiner §8.2)

The symmetric 4f geometry:
```
Input → G1 (grating) → L1 (f) → [Mask plane = Fourier plane] → L2 (f) → G2 (grating) → Output
         |______ f ______|         |____________ f ____________|
```

**Step 1 — spatial dispersion (G1 + L1)**: Grating G1 angularly disperses
the spectrum. Lens L1 maps angle to position at the Fourier plane:
```
x(ω) = f · (λ(ω) − λ₀)/(d cos θ_d)
```
Each wavelength focuses to a unique transverse position — a 1D spatial-to-
spectral mapping.

**Step 2 — spectral filtering (mask)**: At the Fourier plane, apply:
```
M(ω) = amplitude mask (0 to 1)
φ(ω) = phase mask (0 to 2π)
Ẽ_out(ω) = M(ω) e^{iφ(ω)} Ẽ_in(ω)
```

**Step 3 — recombination (L2 + G2)**: Lens L2 and grating G2 undo the
spatial dispersion, recombining the shaped spectrum into a single output
beam.

**Output pulse** (Fourier synthesis):
```
a_out(t) = F⁻¹{M(ω) e^{iφ(ω)} F{a_in(t)}}
```

### 2. Mask technologies

**Liquid Crystal Spatial Light Modulator (LC-SLM)**:
- 640 or 1280 pixels, each with independently addressable voltage.
- Voltage controls birefringence → phase shift 0-2π per pixel.
- Pixel gaps (∼2-3 μm) cause diffraction loss and replica pulses.
- Update rate: ∼10-100 Hz (nematic) or ∼kHz (ferroelectric).
- Dual-mask design: separate amplitude and phase control (polarizer + 2 SLMs).

**Acousto-Optic Modulator (AOM, Dazzler)**:
- RF waveform launched into AOM crystal → traveling acoustic grating.
- Collinear geometry: signal and acoustic wave co-propagate → phase-matched
  diffraction → shaped output.
- Continuous (no pixelation), high update rate (∼kHz), limited time window.

### 3. Spectral resolution and space-time coupling

**Spectral resolution** (Rayleigh criterion at Fourier plane):
```
δλ = (λ² d cos θ_in) / (f N_g)
```
where N_g is the number of illuminated grating lines. For 1200 l/mm grating,
f = 20 cm, 5 mm beam: N_g ≈ 6000 lines → δλ ≈ 0.03 nm at 800 nm.

**Space-time coupling**: The output pulse has different spatial profiles at
different times because different wavelengths (spatially separated at mask)
arrive at different times. For simple phase masks this is negligible; for
amplitude masks with sharp spectral edges, space-time coupling degrades
focusability.

### 4. Frequency-to-time mapping (far-field regime)

When the shaper applies a LARGE quadratic spectral phase ψ₂ ≫ τ_p²:
```
a_out(t) ∝ Ẽ_in(ω = (t − τ_g)/ψ₂)     [frequency-to-time mapping]
```
The temporal intensity directly mirrors the spectral intensity — the basis
of arbitrary optical waveform generation. This is the time-domain analog
of Fraunhofer diffraction.

### 5. MIIPS — adaptive compression (Dantus §4)

MIIPS uses the shaper to apply reference phase functions φ_ref(ω;α) and
monitors the SHG spectrum. The SHG signal is maximal when φ_ref cancels
the pulse's intrinsic spectral phase. By scanning over a basis set of
sinusoidal phase functions, MIIPS retrieves and compensates φ(ω) in a
single measurement-compensation cycle.

## Algorithm — Given Target Waveform → Shaper Design

```
1. SPECIFY target: a_target(t) or I_target(t). Compute target spectrum.

2. COMPUTE MASK:
   Ẽ_target(ω) = F{a_target(t)}
   M(ω) = |Ẽ_target(ω)| / |Ẽ_in(ω)|   [amplitude mask]
   φ(ω) = arg(Ẽ_target(ω)) − arg(Ẽ_in(ω))   [phase mask]

3. CHECK FEASIBILITY:
   - M(ω) ≤ 1 for all ω (passive loss only — no gain in shaper).
     If M > 1, scale down → lower output energy.
   - φ_max variation within [0,2π] range of SLM.
   - Spectral resolution δλ: features in mask must be >δλ.

4. UPLOAD to SLM: convert M(ω) and φ(ω) to pixel voltages.
   Account for pixel-to-wavelength calibration, voltage-phase response.

5. MEASURE output (FROG/SPIDER). Compare to target.
   Iterate if needed (closed-loop shaping).

6. For adaptive compression: MIIPS scan → retrieve φ_in(ω) → apply
   φ_comp(ω) = −φ_in(ω) + φ_target(ω).
```

## Edge Cases

- **Pixelation artifacts**: SLM pixel gaps create replica pulses at
  delays Δt = 2π/Δω_pixel. Reduce by using as many pixels as possible.
- **Amplitude mask efficiency**: Amplitude-only shaping discards energy
  in blocked spectral components. Use phase-only shaping when possible.
- **Voltage-phase calibration drift**: LC-SLM response changes with
  temperature. Recalibrate periodically.
- **Space-time coupling for sub-10 fs pulses**: For octave-spanning spectra,
  the lens chromatic aberration and grating non-uniform efficiency produce
  significant space-time coupling. Design with reflective optics (Öffner
  triplet or cylindrical mirrors).

## Cross-References

- Weiner §8, Dantus §2-5
- ultrafast-optics: reasoning.uo.pulse_propagation_linear (pulse FT representation)
- ultrafast-optics: reasoning.uo.pulse_characterization_spider_dscan (MIIPS retrieval)
- ultrafast-optics: reasoning.uo.dispersion_compensation (pulse shaper as programmable GDD)
