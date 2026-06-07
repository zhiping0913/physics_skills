---
node_type: knowledge
domain: ultrafast-optics
topic: ultrafast_spectroscopy_methods
tags: [pump-probe, photon echo, 2D spectroscopy, transient absorption, T1, T2, dephasing, coherent control]
citations:
  - "Weiner, §12-13"
  - "Diels-Rudolph, §8"
  - "Mukamel, Principles of Nonlinear Optical Spectroscopy (1995)"
---

# Ultrafast Spectroscopy Methods — Implementation Guide

## Technique Comparison

| Technique | # pulses | What is measured | Information | Time resolution |
|-----------|---------|-----------------|-------------|----------------|
| Pump-probe | 2 | ΔT(τ), ΔA(λ,τ) | Population dynamics (T₁), spectral evolution | ∼τ_pulse (10-100 fs) |
| Transient grating | 2 (crossed) | Diffracted signal ∝ |χ⁽³⁾|² | T₁, T₂, thermal diffusion | ∼τ_pulse |
| Photon echo (2-pulse) | 2 | Echo intensity vs τ | T₂ (homogeneous dephasing) | ∼τ_pulse |
| Photon echo (3-pulse) | 3 | Echo vs τ₁₂, T | T₂, T₁, spectral diffusion | ∼τ_pulse |
| 2D electronic (2DES) | 3+LO | S(ω_τ, T, ω_t) | Couplings, energy transfer, coherences | ∼10 fs |
| 2D IR (2DIR) | 3 (IR) | S(ω_pump, T, ω_probe) | Vibrational couplings, structure | ∼50 fs |
| Coherent control | 2+shaper | Product yield vs phase | Quantum interference pathways | ∼τ_pulse |
| THz spectroscopy | 1 THz + 1 probe | E_THz(t) via EO sampling | Conductivity, phonons, free carriers | ∼50 fs |

## Typical Molecular Timescales

| Process | Timescale | Technique |
|---------|----------|-----------|
| Electronic dephasing (T₂) in solution | 10-100 fs | Photon echo, 2DES |
| Vibrational dephasing (T₂) | 0.5-10 ps | 2DIR |
| Solvation dynamics | 50 fs–10 ps | Dynamic Stokes shift |
| Electronic energy transfer (EET) | 100 fs–100 ps | Pump-probe, 2DES |
| Electron transfer (ET) | 100 fs–ns | Pump-probe, TA |
| Photoisomerization | 200 fs–10 ps | Pump-probe, 2DES |
| Intersystem crossing (ISC) | ps–μs | TA, phosphorescence |
| Fluorescence lifetime (T₁) | ps–ns | TCSPC, streak camera, upconversion |
| Vibrational relaxation (IVR) | 1-10 ps | Pump-probe, 2DIR |
| Spectral diffusion | 1 ps–1 ns | 3-pulse echo, 2D lineshape |

## 2D Spectroscopy Phase Cycling

For 2D spectroscopy with three pulses (wavevectors k₁,k₂,k₃), the desired
signal directions are:
```
Rephasing:      k_sig = −k₁ + k₂ + k₃   (photon echo)
Non-rephasing:  k_sig = +k₁ − k₂ + k₃
```
Phase cycling: vary the phase of each pulse by φ_i = 0, π, π/2, 3π/2,
and combine signals to isolate the desired nonlinear response.

**Pulse ordering**: pulse 1 and 2 MUST arrive before pulse 3 (causality):
τ = t₂ − t₁ > 0, T = t₃ − t₂ > 0. Accidental pre-pulse signals are
removed by phase cycling.

## Transient Absorption Data Analysis

**Global analysis**: Fit ΔA(λ,t) to a sum of exponential decay components:
```
ΔA(λ,t) = Σ_i D_i(λ) exp(−t/τ_i) + D_∞(λ)
```
where D_i(λ) are decay-associated difference spectra (DADS). Evolution-
associated difference spectra (EADS) for sequential models: A→B→C→...

**Singular value decomposition (SVD)**: ΔA matrix → U S V^T. Number of
significant singular values = number of spectrally distinct components.

## Common Experimental Artifacts

| Artifact | Cause | Mitigation |
|----------|-------|-----------|
| Coherent artifact (t=0 spike) | Cross-phase modulation, solvent Kerr | Magic angle polarization (54.7°), solvent subtraction |
| Thermal lensing | Sample heating by pump | Flow cell, low rep rate, chopping |
| Sample degradation | Photodamage | Flow cell, N₂ purging, fresh sample |
| Group velocity dispersion | Different λ travel at different v_g in sample/solvent | Compensate with prisms, thin sample |
| Scattering | Bubbles, aggregates | Filter sample, flow cell |
| Detector nonlinearity | Saturation of photodiode/CCD | Attenuate, calibrate linear range |

## Chirp Correction in Broadband Probing

A white-light supercontinuum probe has intrinsic chirp (red leads blue
in most materials). This causes different probe wavelengths to sample
different pump-probe delays. Correction:
```
t(λ) = t₀ + a(λ−λ₀) + b(λ−λ₀)² + ...   (chirp polynomial)
```
Determine by: (1) coherent artifact at t=0 in pure solvent, (2) optical
Kerr gate measurement of chirp. Fit chirp polynomial and interpolate data
to common delay grid.

## Key Optical Coherence Parameters

| Parameter | Symbol | Relation | Typical Range |
|-----------|--------|---------|--------------|
| Dephasing time | T₂ | 1/T₂ = 1/(2T₁) + 1/T₂* | 10-100 fs (electronic), 1-10 ps (vibrational) |
| Pure dephasing | T₂* | From homogeneous broadening Γ_hom = 1/(πT₂*) | 20-200 fs |
| Population time | T₁ | Fluorescence/excited-state lifetime | ps-ns (electronic), ps (vibrational) |
| Inhomogeneous width | σ_inh | Gaussian width of static distribution | 50-500 cm⁻¹ |
| FFCF | C(t) | Frequency fluctuation correlation function | Decays with spectral diffusion time |
