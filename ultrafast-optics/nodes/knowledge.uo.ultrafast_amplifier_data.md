---
node_type: knowledge
domain: ultrafast-optics
topic: ultrafast_amplifier_data
tags: [CPA, OPCPA, Ti:sapphire, Yb:fiber, Nd:glass, PW, B-integral, gain narrowing, contrast]
citations:
  - "Weiner, §11"
  - "Diels-Rudolph, §7"
---

# Ultrafast Amplifier Data — System Parameters and Scaling

## Ti:sapphire CPA Systems

| Parameter | kHz System | 10 Hz System | PW System |
|-----------|-----------|-------------|-----------|
| Pulse energy | 1-10 mJ | 1-5 J | 30-300 J |
| Repetition rate | 1-10 kHz | 10 Hz | 0.1-1 Hz |
| Compressed τ | 20-30 fs | 25-50 fs | 20-30 fs |
| Peak power | 0.05-0.5 TW | 20-200 TW | 1-10 PW |
| Average power | 5-50 W | 10-50 W | 3-30 W |
| Stretcher ratio | 10³-10⁴ | 10⁴ | 10⁴-10⁵ |
| B-integral (total) | 1-2 | 2-4 | 3-5 |
| Contrast (ASE) | 10⁻⁵-10⁻⁶ | 10⁻⁶-10⁻⁷ | 10⁻⁷-10⁻⁸ |
| Beam size (compressor) | 10-20 mm | 50-100 mm | 200-400 mm |
| Grating size | 20-50 mm | 100-200 mm | 400-940 mm |

## Ti:sapphire Gain Medium Properties

| Property | Value |
|----------|-------|
| Gain peak λ | 800 nm |
| Bandwidth (FWHM) | Δλ ≈ 120 nm, Δν ≈ 100 THz |
| Emission cross-section σ_em | 3×10⁻¹⁹ cm² |
| Upper-state lifetime τ_f | 3.2 μs |
| Saturation fluence F_sat | 0.9 J/cm² |
| n₂ (Kerr) | 3×10⁻¹⁶ cm²/W |
| Thermal conductivity | 33 W/(m·K) (∥c) |
| Figure of merit (FOM) | >150 for low-loss |
| Doping concentration | 0.1-0.25 wt% Ti₂O₃ |
| Pump wavelength | 532 nm (frequency-doubled Nd:YAG/YLF) |
| Quantum defect | 34% |

## Yb-doped CPA Systems

| Parameter | Yb:YAG (thin-disk) | Yb:fiber | Yb:CaF₂ |
|-----------|-------------------|----------|---------|
| λ_center | 1030 nm | 1030 nm | 1030 nm |
| Δλ (FWHM) | 6-10 nm | 20-40 nm | 60-80 nm |
| τ_comp (best) | 400-800 fs | 100-300 fs | 50-100 fs |
| E_pulse (max) | 100 mJ | 1-10 mJ | 100 mJ |
| P_avg (max) | 1 kW | 100 W | 50 W |
| f_rep | 10-100 kHz | 1-100 MHz | 1-10 kHz |
| σ_em | 2×10⁻²⁰ cm² | 3×10⁻²⁰ cm² | 1.7×10⁻²⁰ cm² |
| τ_f | 1 ms | 0.8 ms | 2 ms |

## OPCPA System Parameters

| Parameter | Few-cycle OPCPA | High-energy OPCPA | PW OPCPA |
|-----------|----------------|-------------------|----------|
| Crystal | BBO (Type I) | LBO / DKDP | DKDP |
| λ_signal | 700-900 nm | 800-1050 nm | 910-1050 nm |
| λ_pump | 532 nm (Nd:YAG) | 527 nm (Nd:YLF) | 527 nm |
| τ_pump | 10-100 ps | 100-500 ps | 1-10 ns |
| τ_compressed | 3.5-7 fs | 10-20 fs | 15-30 fs |
| E_out | 0.1-10 mJ | 1-10 J | 30-100 J |
| P_peak | GW-TW | TW | 1-10 PW |
| Contrast | >10¹⁰ | >10⁸ | >10⁸ |
| Conversion efficiency | 20-30% | 30-40% | 40-60% |

## Gain Narrowing — Practical Formula

For Ti:sapphire multi-pass amplifier with total gain G₀:
```
Δλ_out = Δλ_in / √(1 + ln G₀ × (Δλ_in/Δλ_g)²)
```
| ln G₀ | Δλ_out for Δλ_in=Δλ_g=120 nm |
|-------|------------------------------|
| 5 | 49 nm |
| 10 | 36 nm |
| 15 | 30 nm |
| 20 | 26 nm |

For Δλ_out = 100 nm → τ_TL ≈ 9 fs. For Δλ_out = 30 nm → τ_TL ≈ 31 fs.

## B-integral Guidelines

| B | Effect | Action |
|---|--------|--------|
| <1 | Negligible | OK |
| 1-2 | Minor temporal modulation, correctable | Monitor |
| 2-3 | Significant SPM, beam break-up at edges | Increase stretcher ratio |
| 3-5 | Severe distortion, pre-pulses from SPM | Re-design |
| >5 | Catastrophic, beam filamentation | Must avoid |

## PW-class Laser Facilities (2025)

| Facility | Country | P_peak | E_pulse | τ_pulse | f_rep |
|----------|---------|--------|---------|---------|-------|
| ELI-NP (HPLS) | Romania | 10 PW | 220 J | 22 fs | 1/min |
| ELI-ALPS (SYLOS) | Hungary | 4.5 PW | 55 J | 12 fs | 1 Hz |
| Apollon | France | 5 PW | 150 J | 30 fs | 1/min |
| SULF | China | 10 PW | 300 J | 30 fs | 1/min |
| CoReLS | Korea | 4 PW | 80 J | 20 fs | 0.1 Hz |
| BELLA | USA | 1 PW | 40 J | 40 fs | 1 Hz |
