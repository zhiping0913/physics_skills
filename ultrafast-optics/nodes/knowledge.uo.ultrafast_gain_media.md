---
node_type: knowledge
domain: ultrafast-optics
topic: ultrafast_gain_media
tags: [Ti:sapphire, Yb:doped, Cr:forsterite, Er:fiber, Yb:fiber, semiconductor, VECSEL, MIXSEL, gain bandwidth, emission cross-section, thermal conductivity]
citations:
  - "Weiner, §1, §6-7"
  - "Diels-Rudolph, §4"
  - "Siegman, §7, §27"
---

# Ultrafast Gain Media — Properties and Selection

## Broadband Solid-State Crystals

| Medium | λ_center (nm) | Δλ_FWHM (nm) | Δν (THz) | τ_TL_min (fs) | σ_em (10⁻²⁰ cm²) | τ_f (μs) | n₂ (10⁻¹⁶ cm²/W) | κ (W/m·K) |
|--------|--------------|-------------|----------|--------------|-------------------|----------|-----|-----|
| **Ti:sapphire** (Ti:Al₂O₃) | 790 | 120-150 | 100 | 3-5 | 30-40 | 3.2 | 3.0 | 33 |
| **Cr:LiSAF** | 850 | 100 | 55 | 9 | 5 | 67 | 0.5 | 3 |
| **Cr:forsterite** | 1250 | 100 | 24 | 20 | 15 | 2.7 | 1.5 | 8 |
| **Cr:ZnSe** | 2450 | 400 | 20 | 115 | 90 | 8 | — | 18 |
| **Alexandrite** | 750 | 100 | 50 | 10 | 1.5 | 260 | — | 23 |

**Ti:sapphire** is the gold standard: broadest bandwidth of any laser crystal
(Δν ∼ 100 THz → τ_TL ∼ 4 fs), high thermal conductivity, excellent figure of
merit. Pumped by 532 nm (frequency-doubled Nd:YAG/Nd:YVO₄) or 488-514 nm (Ar⁺).

## Yb-doped Gain Media (~1 μm)

| Medium | λ_center | Δλ (nm) | τ_TL (fs) | σ_em | τ_f (ms) | κ (W/m·K) | Key Feature |
|--------|---------|---------|----------|------|----------|-----|------------|
| Yb:YAG (bulk) | 1030 | 6-10 | 160 | 2 | 1.0 | 11 | High avg power (thin-disk) |
| Yb:KYW | 1030 | 20-25 | 50 | 3 | 0.3 | 3.3 | Broadband, low τ_f |
| Yb:KGW | 1040 | 20-25 | 50 | 3 | 0.3 | 3 | Raman-active |
| Yb:CaF₂ | 1040 | 60-80 | 18 | 1.7 | 2.4 | 10 | Broadest Yb bandwidth |
| Yb:glass | 1030 | 30-40 | 30 | 0.05 | 2 | 0.8 | Fiber-compatible |
| Yb:Lu₂O₃ | 1032 | 13 | 90 | 1.2 | 0.8 | 13 | Highest κ for Yb |
| Yb:fiber | 1030 | 20-40 | 30 | 3 | 0.8 | 1.4 | Diffraction-limited beam |

Yb advantage over Ti:sapphire: low quantum defect (<10% vs 34%) → low
thermal load → high average power. Yb:YAG thin-disk: >1 kW average power.
Disadvantage: narrower bandwidth → longer pulses (typ. 200-800 fs).

## Fiber Gain Media

| Dopant | λ_center | Δλ (nm) | Application |
|--------|---------|---------|------------|
| **Er³⁺** (silica) | 1550 | 30-40 | Telecom, fs fiber lasers, frequency combs |
| **Er³⁺** (fluoride) | 2750 | 50-100 | Mid-IR fs pulses |
| **Yb³⁺** (silica) | 1030 | 20-40 | High-power fs fiber CPA |
| **Tm³⁺** (silica) | 1900 | 100-200 | 2 μm fs pulses, mid-IR pumping |
| **Ho³⁺** (silica) | 2080 | 50-100 | 2 μm, eye-safe |
| **Nd³⁺** (silica) | 1060 | 10-20 | ps/ns pulses (narrow bandwidth — not fs) |
| **Bi-doped** | 1300 | 50-100 | O-band amplification |

**Soliton self-frequency shift (SSFS) in fibers**: Er soliton at 1550 nm
can Raman-shift continuously to >2000 nm — tunable fs source from a single
fixed-wavelength laser.

## Semiconductor Gain Media

| Type | λ (nm) | τ_p (fs) | P_avg (mW) | f_rep (GHz) | Application |
|------|--------|---------|-----------|------------|------------|
| **VECSEL** (OP-SDL) | 950-1050 | 100-500 | 100-1000 | 1-10 | High-power, diffraction-limited |
| **MIXSEL** | 960 | 200-600 | 10-100 | 1-100 | Integrated ML semiconductor laser |
| **Quantum dot** | 1250 | 200-1000 | 10-50 | 5-50 | Low threshold, broad gain |
| **InGaAs/GaAs QW** | 980-1100 | 200-1000 | 50-500 | 1-20 | Diode-pumped, compact |

## Bandwidth → Pulse Duration

Transform-limited pulse durations for sech² pulses:
| Δλ (nm) at 800 nm | Δν (THz) | τ_TL (fs) |
|-------------------|----------|----------|
| 10 | 4.7 | 67 |
| 30 | 14 | 22 |
| 60 | 28 | 11 |
| 120 | 56 | 5.6 |
| 200 | 94 | 3.4 |
| 400 (octave) | 188 | 1.7 |

**Rule of thumb**: τ_TL(fs) ≈ 1800/Δν(THz) or τ_TL(fs) ≈ 700/(Δλ(nm) at 800 nm).
