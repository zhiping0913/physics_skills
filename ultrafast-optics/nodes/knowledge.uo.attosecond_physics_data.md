---
node_type: knowledge
domain: ultrafast-optics
topic: attosecond_physics_data
tags: [HHG, attosecond, IAP, APT, streaking, cutoff, XUV, RABBITT, FROG-CRAB]
citations:
  - "PUILS-XIII (2017)"
  - "Krausz & Ivanov, Rev. Mod. Phys. 81:163 (2009)"
---

# Attosecond Physics Data

## HHG Cutoff Energies

| Gas | I_p (eV) | I (W/cm²) at 800 nm | U_p (eV) | E_cutoff (eV) | λ_cutoff (nm) |
|-----|---------|--------------------|---------|--------------|-------------|
| Ar | 15.8 | 10¹⁴ | 6.0 | 35 | 35 |
| Ar | 15.8 | 3×10¹⁴ | 18 | 73 | 17 |
| Ne | 21.6 | 5×10¹⁴ | 30 | 117 | 10.6 |
| He | 24.6 | 10¹⁵ | 60 | 215 | 5.8 |
| He | 24.6 | 3×10¹⁵ | 180 | 600 | 2.1 |

**Wavelength scaling**: U_p ∝ λ² → longer driver → higher cutoff at same
intensity. Mid-IR drivers (1.8-4 μm) can reach keV photon energies.

## Attosecond Pulse Duration Records

| Year | Group | τ (as) | Method | Driver |
|------|-------|--------|--------|--------|
| 2001 | Krausz (Vienna) | 650 | APT + filtering | 7 fs Ti:S |
| 2004 | Krausz | 250 | IAP, amplitude gating | 5 fs Ti:S, CEP-stab |
| 2008 | Krausz | 80 | IAP, DOG | 3.3 fs Ti:S, CEP |
| 2012 | Chang (UCF) | 67 | IAP, DOG | 2-cycle Ti:S |
| 2017 | Gaumnitz (ETH) | **43** | IAP, 1.8 μm driver | sub-2-cycle OPA |
| 2022 | Li (ELI) | 53 | IAP, high-flux | Few-cycle, high rep |

**Current record**: 43 attoseconds (∼4.3×10⁻¹⁷ s) — corresponds to ∼15
optical cycles at 100 eV XUV photon energy.

## HHG Phase Matching Conditions

For a gas target of length L_med with pressure P:

**Optimal pressure** (constant absorption):
```
P_opt ≈ (κ_abs L_med)^{-1}
```
where κ_abs is the absorption coefficient at the harmonic wavelength.

**Coherence length** (from phase mismatch Δk):
```
L_coh = π/|Δk|
Δk = Δk_neutral + Δk_plasma + Δk_geometric
Δk_plasma = −(ω_p²)/(2c ω) · (1 − η)   [ionization: η < 1 free electrons add negative Δk]
Δk_geometric = −(1)/(z_R) for Gaussian beam [Gouy phase]
```

For efficient HHG: L_med ≤ 3 L_coh, P ≈ P_opt.

## XUV Optics and Filters

| Material | Transmission band (eV) | Cutoff (eV) | Application |
|----------|----------------------|------------|------------|
| Al | 17-72 | 72 (L-edge) | Low harmonics, Ar HHG |
| Zr | 60-120 | — | Ne HHG cutoff |
| Mo/Si multilayer | 85-95 (10 eV FWHM) | — | 13.5 nm (EUV lithography) |
| Si₃N₄ membrane | <100 eV | — | Broadband XUV window |
| Sn filter | <25 eV | — | Block IR driver |

## Attosecond Streaking Parameters

| Parameter | Value |
|-----------|-------|
| XUV bandwidth required | >10 eV FWHM (for <200 as resolution) |
| IR streaking field | Few-cycle (τ < 6 fs), CEP-stabilized, I ∼ 10¹²-10¹³ W/cm² |
| Target gas | Ne or Ar (∼10⁻³ mbar) |
| Electron spectrometer | Time-of-flight (TOF) with magnetic bottle or velocity map imaging (VMI) |
| Delay step | ∼50-100 as |
| Retrieval | FROG-CRAB (modified GP algorithm) |

## Major Attosecond Facilities

| Facility | Location | Driver | IAP τ | f_rep | XUV energy |
|----------|---------|--------|-------|-------|-----------|
| ELI-ALPS (HR1) | Hungary | 5 PW, few-cycle | <100 as | 1 kHz | 10-100 eV |
| ELI-ALPS (MIR) | Hungary | Mid-IR (3.2 μm) | <200 as | 10 Hz | >500 eV |
| LCLS (X-ray FEL) | USA | Free-electron laser | sub-fs | 120 Hz | 250-2500 eV |
| European XFEL | Germany | FEL | sub-fs | 27 kHz | 250-25000 eV |
| Max Planck (MPQ) | Germany | Few-cycle Ti:S | <100 as | 3 kHz | 10-120 eV |
| Lund (LLC) | Sweden | Few-cycle OPCPA | <100 as | 10 kHz | 10-60 eV |

## RABBITT — Attosecond Pulse Train Characterization

RABBITT measures the relative phase between adjacent harmonic orders:
```
XUV comb (odd harmonics q±1) + IR probe → sidebands at q ω₀ (even)
Sideband modulation vs XUV-IR delay τ:
I_SB(q,τ) = A + B cos(2ω₀τ − Δφ_q)
Δφ_q = φ(q+1) − φ(q−1) → phase difference → attosecond chirp
```
The method provides the GROUP DELAY of the attosecond pulse train,
from which both APT duration and chirp are inferred.
