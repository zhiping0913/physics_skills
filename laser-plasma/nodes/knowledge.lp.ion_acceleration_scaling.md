---
skill_id: knowledge.lp.ion_acceleration_scaling
type: knowledge
summary_50t: >
  TNSA: ε_max ∝ T_hot ln(ω_pi τ_L), T_hot ∝ I^{0.3–0.5}, exponential
  spectrum. RPA: ε ∝ I/n_e d (light-sail), CP required, monoenergetic.
  Experimental records: TNSA → 85 MeV protons (DRACO), RPA → 50 MeV/u
  C⁶⁺ (ELI). Key facilities. Proton radiography applications.
trigger:
  - looking up experimental records for laser-ion acceleration
  - comparing proton energy from TNSA vs RPA
  - designing proton/heavy ion acceleration experiments
parent: reasoning.lp.tnsa_ion_acceleration
retrieval_cost: 1
---

# knowledge.lp.ion_acceleration_scaling — TNSA/RPA Benchmarks

## TNSA Energy Scaling

**Hot electron temperature** (empirical — Beg / ponderomotive scaling):
```
T_hot[MeV] ≈ 0.511 (√(1+a₀²) − 1)      [ponderomotive, Wilks 1992]
T_hot[keV] ≈ 3.6 (I_18 λ_μm²)^{0.42}×10⁴    [Beg scalings, empirical]
T_hot[MeV] ≈ 1.5 (I_20 λ_μm²)^{0.5}         [ultra-relativistic, Fuchs 2006]
```

**Maximum proton energy**:
```
ε_max[MeV] ≈ 2 α T_hot ln(ω_pi τ_L + √(1+ω_pi²τ_L²))
```
where α ≈ 1.5–2.5 depending on target geometry and contaminant thickness.
Simplified: ε_max[MeV] ≈ C (I_20 λ_μm²)^{0.5}, C ≈ 0.3–0.5.

| I (W/cm²) | λ (μm) | T_hot (MeV) | τ_L (fs) | ε_max^p (MeV) | Notes |
|-----------|--------|-------------|----------|--------------|-------|
| 10¹⁸ | 1 | 0.5 | 500 | 2 | Early TNSA |
| 10¹⁹ | 1 | 1.5 | 500 | 8 | — |
| 10²⁰ | 1 | 5 | 500 | 30 | — |
| 5×10²⁰ | 1 | 12 | 500 | 60 | — |
| 10¹⁹ | 1 | 1.5 | 100 | 3 | Short pulse |
| 10²⁰ | 0.4 | 8 | 500 | 40 | UV driver |

## TNSA Experimental Records

| Year | Facility | I (W/cm²) | λ (μm) | ε_max (MeV) | Ion | Notes |
|------|----------|----------|--------|-------------|-----|-------|
| 2000 | NOVA PW | 3×10²⁰ | 1.05 | 58 | p | Snavely et al. |
| 2006 | LULI | 6×10¹⁹ | 1.05 | 34 | p | Fuchs et al. |
| 2011 | TRIDENT | 2×10²⁰ | 1.05 | 67 | p | Flippo et al. |
| 2019 | DRACO | 10²¹ | 0.8 | 85 | p | Obst et al. |
| 2023 | ELI NP | 10²¹ | 0.8 | ~100 | p | Recent |

**High-Z ion acceleration via TNSA**:
| Year | Ion | ε_max (MeV/u) | Facility |
|------|-----|--------------|----------|
| 2004 | C⁶⁺ | 5 | LULI |
| 2008 | Au⁵⁰⁺ | 0.5 | TRIDENT |
| 2013 | C⁶⁺ | 15 | LANL |

## RPA (Light-Sail) Energy Scaling

```
ε_i[MeV/u] ≈ 2 × 10⁻⁴ I_20 τ_L[fs] / σ[μg/cm²]    [non-relativistic]
```

| I (W/cm²) | τ_L (fs) | σ (μg/cm²) | ε_i (MeV/u) | Notes |
|-----------|----------|------------|------------|-------|
| 5×10¹⁹ | 30 | 10 | 30 | DLC foil |
| 10²⁰ | 50 | 5 | 200 | CNT foil |
| 5×10²⁰ | 30 | 1 | 3000 | Ultra-thin foil |
| 10²² | 20 | 5 | 8000 | ELI-NP goal |

## RPA Experimental Benchmarks

| Year | Facility | Ion | ε_max (MeV/u) | Regime | Notes |
|------|----------|-----|--------------|--------|-------|
| 2008 | Jena | p | 13 | HB-RPA | Henig et al. |
| 2011 | TRIDENT | C⁶⁺ | 25 | LS-RPA | Kar et al. |
| 2015 | J-KAREN | C⁶⁺ | 50 | LS-RPA | — |
| 2018 | ELI | p | 94 | HB-RPA (prelim) | — |

## TNSA Spectrum Shape

Exponential: dN/dε ∝ exp(−ε/T_hot) with cutoff at ε_max.
Proton number: ~10¹² protons/MeV at 1 MeV, ~10⁸ at 10 MeV (for I~10²⁰ W/cm²).
The exponential shape is intrinsic to isothermal expansion; achieving
monoenergetic spectra requires RPA or spectral filtering.

## Proton Radiography Applications

TNSA proton beams are used for:
- **Electric/magnetic field imaging**: deflection by E/B fields in plasma →
  proton radiograph. Resolution ~few μm, temporal resolution ~ps.
- **Fast ignition**: proton beam heats compressed DT fuel → ignition spark.
- **Medical isotope production**: ¹⁸F, ¹¹C production via (p,n) reactions.
- **Materials science**: high dose-rate irradiation studies.

## Key Ion Acceleration Facilities

| Facility | P (TW) | I_max (W/cm²) | Target type | ε_max (MeV) |
|----------|--------|--------------|-------------|-------------|
| DRACO (HZDR) | 150 | 5×10²⁰ | TNSA | 85 (p) |
| PHELIX (GSI) | 500 | 10²¹ | TNSA | 60 (p) |
| ELI-NP (Romania) | 10 PW | 10²² | RPA/LS | target: 200 (p) |
| SULF (Shanghai) | 500 | 10²¹ | TNSA/RPA | — |
| BELLA PW | PW | 5×10²¹ | TNSA | — |

## Cross-References

- laser-plasma: reasoning.lp.tnsa_ion_acceleration (parent — TNSA theory)
- laser-plasma: reasoning.lp.radiation_pressure_acceleration (RPA theory)
- laser-plasma: knowledge.lp.electron_acceleration_scaling (electron acceleration benchmarks for comparison)
