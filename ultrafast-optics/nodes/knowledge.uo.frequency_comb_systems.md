---
node_type: knowledge
domain: ultrafast-optics
topic: frequency_comb_systems
tags: [frequency comb, f-2f, optical clock, dual-comb, metrology, Sr clock, Yb clock]
citations:
  - "Ye-Cundiff, Femtosecond Optical Frequency Comb (2005)"
---

# Frequency Comb Systems — Implementation Data

## Comb Source Technologies

| Platform | λ_center | f_rep range | Δν_comb | Stability |
|----------|---------|-----------|---------|-----------|
| Ti:sapphire (PCF broadened) | 800 nm | 80 MHz–1 GHz | Octave (500-1100 nm) | Excellent |
| Er:fiber (HNLF broadened) | 1550 nm | 100–250 MHz | Octave (1000-2200 nm) | Good (environmentally robust) |
| Yb:fiber | 1030 nm | 80–250 MHz | 2/3 octave | Good |
| Microresonator (Kerr comb) | 1550 nm | 10–1000 GHz | Octave | Chip-scale |
| Quantum cascade laser (QCL) | 4-12 μm | 5-20 GHz | Limited (∼100 cm⁻¹) | Developing |

## f-2f Interferometer Designs

**Common-path f-2f** (fiber-based):
```
Comb → PCF (supercontinuum) → long-pass (λ > 900 nm) → PPLN SHG → 
                                                               ↓
       short-pass (λ < 550 nm) → delay line → BS → PD → f_CEO
```
- PPLN (periodically-poled LiNbO₃) for efficient SHG
- Delay line matches path lengths to fs precision
- PD bandwidth: > f_rep to resolve f_CEO

**f-2f beat note properties**:
- SNR: 30-40 dB (100 kHz RBW) for octave-spanning Ti:sapphire comb
- SNR: 20-30 dB for Er:fiber comb
- f_CEO linewidth (free-running): ∼1-10 MHz (limited by pump noise + cavity fluctuations)
- f_CEO linewidth (locked): <1 Hz (limited by reference oscillator)

## Comb Stabilization Electronics

| Parameter | f_rep lock | f_CEO lock |
|-----------|-----------|-----------|
| Actuator | PZT + motor | Pump current/power |
| Bandwidth | ∼10 kHz | ∼100 kHz |
| Reference | RF synthesizer | RF synthesizer (f_CEO ref) |
| Loop filter | PI²D (2 integrators) | PID |
| Residual phase noise | <100 mrad (1 Hz–1 MHz) | <200 mrad |

## Optical Atomic Clocks

| Clock transition | Atom/Ion | λ (nm) | Q factor | Fractional uncertainty |
|-----------------|---------|--------|---------|----------------------|
| ¹S₀→³P₀ | ⁸⁷Sr | 698 | 10¹⁷ | 2×10⁻¹⁸ |
| ¹S₀→³P₀ | ²⁷Al⁺ | 267 | 10¹⁷ | 1×10⁻¹⁸ |
| ²S₁/₂→²F₇/₂ | ¹⁷¹Yb⁺ | 467 | 10¹⁵ | 3×10⁻¹⁸ |
| ¹S₀→³P₀ | ¹⁷¹Yb | 578 | 10¹⁶ | 2×10⁻¹⁸ |
| ²S₁/₂→²D₅/₂ | ⁴⁰Ca⁺ | 729 | 10¹⁴ | 1×10⁻¹⁷ |

The ¹⁷¹Yb⁺ octupole (E3) transition has extremely low sensitivity to
external field perturbations → potentially 10⁻¹⁹ ultimate accuracy.

## Dual-Comb Spectroscopy Parameters

| Parameter | Near-IR (1.5 μm) | Mid-IR (3-5 μm) |
|-----------|-----------------|-----------------|
| Comb sources | Er:fiber ×2 | OPO-pumped or QCL |
| f_rep | 100-250 MHz | 100 MHz |
| Δf_rep | 10-1000 Hz | 10-100 Hz |
| Resolution | Δf_rep ∼ 10 Hz (1.6×10⁻⁴ cm⁻¹) | Same |
| Acquisition time | 1/Δf_rep ∼ 0.1 s per spectrum | Same |
| Spectral coverage | 100 THz (∼3000 cm⁻¹) | 30 THz (∼1000 cm⁻¹) |
| SNR per spectral element | ∼1000 in 1 s | ∼100-500 |
| Figure of merit | 10⁶ resolution elements × 10³ SNR | — |

## Key Comb Parameters for Metrology

| Parameter | Target |
|-----------|--------|
| f_CEO stability (Allan dev at 1s) | <10⁻¹⁵ |
| Comb tooth linewidth | <1 Hz |
| Comb tooth position uncertainty | <10⁻¹⁸ fractionally |
| Phase noise floor | <−120 dBc/Hz at 1 kHz offset |
| Link to Cs fountain clock | <10⁻¹⁶ uncertainty |

## Practical f_CEO Detection Challenges

**Supercontinuum coherence**: The supercontinuum generated in PCF must be
coherent (low RIN — relative intensity noise). Coherence degrades for long
pulses (>200 fs) and high soliton order. Use short input pulses (<100 fs)
and short PCF length (<10 cm).

**Flicker noise floor**: f_CEO phase noise at low Fourier frequencies is
dominated by flicker (1/f) noise from pump laser and environmental
fluctuations. Requires >10 kHz lock bandwidth or feed-forward cancellation.
