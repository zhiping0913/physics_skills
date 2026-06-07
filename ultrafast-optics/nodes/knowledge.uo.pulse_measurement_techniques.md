---
node_type: knowledge
domain: ultrafast-optics
topic: pulse_measurement_techniques
tags: [FROG, SPIDER, d-scan, autocorrelation, GRENOUILLE, MIIPS, streaking, attosecond, pulse characterization]
citations:
  - "Trebino, FROG (2000)"
  - "Weiner, Ultrafast Optics, §9"
  - "Diels-Rudolph, Ultrashort Laser Pulse Phenomena, §10"
---

# Pulse Measurement Techniques — Taxonomy and Selection

## Classification

| Technique | Domain | What is measured | Retrieval | Single-shot |
|-----------|--------|-----------------|-----------|-------------|
| Intensity autocorrelation | Time | τ_ac (width, no phase) | Analytic (width only) | Yes |
| Interferometric autocorrelation | Time | τ_ac + fringe contrast | Analytic (partial phase) | Yes |
| SHG-FROG | Time-Freq | I_SHG(ω,τ) | GP iterative | GRENOUILLE |
| PG-FROG | Time-Freq | I_PG(ω,τ) | GP iterative | No |
| XFROG | Time-Freq | I_XFROG(ω,τ) | GP iterative | No |
| SPIDER | Frequency | Interferogram I(ω) | Direct analytic | Yes |
| SEA-SPIDER | Frequency | Spatially encoded SPIDER | Direct analytic | Yes |
| d-scan | Frequency | I_SH(ω,GDD_add) | Iterative or MIIPS | No |
| MIIPS | Frequency | I_SH(ω,α,δ) | Analytic comparison | No |
| Attosecond streaking | Time | Electron spectrogram vs τ | FROG-like | Yes |
| Stereo-ATI | Time | Photoelectron angular distribution | Phase-retrieval | Yes |

## Technique Selection by Pulse Regime

### Oscillator-level pulses (τ_p > 20 fs, E_p ∼ nJ)
**Recommended**: SHG-FROG or GRENOUILLE.
- SHG-FROG: high sensitivity, standard. Symmetric trace → time ambiguity.
- GRENOUILLE: alignment-free single-shot version. Same physics.
- d-scan: if the compressor (wedge pair) is already in the beam path.
- SPIDER: if complex temporal structure suspected (satellites, pre/post pulses).

### Amplified few-cycle pulses (τ_p < 10 fs, E_p ∼ μJ−mJ)
**Recommended**: SPIDER or d-scan.
- SPIDER: resolves satellite pulses, direct retrieval.
- d-scan: self-calibrating (compressor IS the measurement device).
- SHG-FROG: thin crystal required (<10 μm); phase-matching bandwidth limits.
- PG-FROG: needs μJ pulses (χ⁽³⁾ sensitivity limit).

### Attosecond pulses (τ_p ∼ as, E ∼ nJ, XUV)
**Recommended**: Attosecond streaking.
- Streaking: IR dressing field streakes photoelectrons → spectrogram.
- FROG-CRAB retrieval algorithm (attosecond FROG variant).
- RABBITT (Reconstruction of Attosecond Beating By Interference of Two-photon Transitions): XUV + IR → sideband interferometry.

## Practical Guidelines

**Autocorrelation is NOT enough**: An autocorrelation trace gives only an
upper bound on pulse duration, assuming a pulse shape. It cannot detect
satellite pulses, pre/post pulses, or spectral phase. FROG/SPIDER/d-scan
is required for complete characterization.

**Thin crystal rule for SHG**: For accurate SHG-based measurements,
the SHG crystal thickness t must satisfy:
```
t < τ_p · v_g / |1/v_g(ω₀) − 1/v_g(2ω₀)|    (GVM length)
```
For 10 fs Ti:sapphire pulses: t < 20 μm (BBO Type I).

**Chirp sign convention**: All FROG/SPIDER/d-scan measurements must specify
the chirp sign convention. Standard ultrafast convention: positive chirp =
red leads blue (dω/dt > 0). FROG traces can distinguish up-chirp from
down-chirp for PG-FROG and THG-FROG, but NOT for SHG-FROG.
