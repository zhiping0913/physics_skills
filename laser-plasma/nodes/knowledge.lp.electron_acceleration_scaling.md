---
skill_id: knowledge.lp.electron_acceleration_scaling
type: knowledge
summary_50t: >
  LWFA and DLA scaling laws: LWFA ε_max ∝ a₀ n_c/n_e, E_wake ∝ √(n_e).
  DLA ε ∝ a₀^{2/3}, betatron X-ray ℏω_c ∝ γ²ω_p. Experimental records:
  8 GeV in 20 cm (LWFA bubble), multi-GeV staged. Key facilities: BELLA,
  Astra-Gemini, SULF. Betatron X-ray sources: keV–MeV, fs duration.
trigger:
  - computing expected electron energy from given laser parameters
  - comparing LWFA and DLA energy scaling predictions
  - looking up experimental benchmarks for electron acceleration
parent: reasoning.lp.laser_wakefield_acceleration
retrieval_cost: 1
---

# knowledge.lp.electron_acceleration_scaling — Energy Scalings & Benchmarks

## LWFA Energy Scaling — Summary

| Regime | Condition | Wake amplitude | Energy scaling | Dephasing length |
|--------|-----------|---------------|---------------|-----------------|
| Linear | a₀ ≪ 1, τ_L ≈ λ_p/2c | E_wake ∝ a₀² | ε ∝ a₀² (n_c/n_e) | L_d = γ_ph² λ_p |
| Quasi-nonlinear | 1 ≲ a₀ ≲ 2 | E_wake ∝ a₀ | ε ∝ a₀ (n_c/n_e) | — |
| Bubble (3D) | a₀ ≳ 2 | E_wake ∝ √a₀ √(n_e) | ε ∝ a₀ (n_c/n_e) | L_d ∝ √a₀ (n_c/n_e)λ_p |
| Bubble (matched) | a₀ ∝ 1/√n_e | P_laser = P_c matched | ε ∝ a₀ (n_c/n_e) | L_d ≈ L_pd |

Practical formula (Lu 2007 bubble scaling):
```
ε[GeV] ≈ 1.7 a₀ (n_c/n_e)
L_d[mm] ≈ 0.7 √a₀ / (n_e/10¹⁸)
```

For a₀=4, n_e=3×10¹⁸ cm⁻³, λ₀=0.8μm: ε≈3.1 GeV, L_d≈2.9 mm.

## LWFA Experimental Benchmarks

| Year | Lab | a₀ | n_e (cm⁻³) | L (mm) | ε (GeV) | Δε/ε | Charge (pC) |
|------|-----|-----|------------|--------|---------|------|------------|
| 2004 | LOA | 2 | 6×10¹⁸ | 3 | 0.17 | 24% | 5 |
| 2006 | LBNL | 4 | 3×10¹⁸ | 3.3 | 1.0 | 2.5% | 30 |
| 2013 | LBNL | 4 | 1×10¹⁸ | 9 | 3.0 | 5% | 10 |
| 2014 | LBNL | 10 | 3×10¹⁷ | 9 | 4.2 | 6% | 6 |
| 2019 | LBNL (BELLA) | — | 5×10¹⁷ | 20 | 7.8 | few% | 5 |
| 2023 | SULF | — | 2×10¹⁸ | 30 | 8+ | — | — |

Key trend: ε_max ∝ 1/n_e (dephasing-limited). Lower density → longer
dephasing length → higher energy, but requires more laser power.

## DLA Scaling

| Parameter | Scaling |
|-----------|---------|
| Resonance condition | ω_D = ω_β |
| Energy scaling | ε ∝ a₀^{2/3} |
| Channel requirement | Self-channeling or pre-formed channel |
| Spectrum shape | Exponential (quasi-thermal) |
| Accompanying radiation | Betatron X-rays |

**DLA vs LWFA dominance**:
- a₀ ≲ 2, τ_L > λ_p/c: DLA can dominate (Pukhov 1999)
- a₀ ≳ 3, τ_L ≈ λ_p/2c: LWFA bubble dominates
- Intermediate: both contribute, broad electron spectrum

## Betatron X-ray Source Parameters

| Facility | a₀ | n_e (cm⁻³) | ε_e (MeV) | ℏω_c (keV) | Photons/shot | Pulse (fs) |
|----------|-----|------------|-----------|------------|-------------|------------|
| LOA (2004) | 2 | 10¹⁹ | 55 | 2 | 10⁸ | ~10 |
| LBNL (2008) | 3 | 10¹⁹ | 100 | 10 | 10⁹ | ~5 |
| ASTRA (2012) | 5 | 10¹⁹ | 200 | 50 | 10⁸ | ~5 |

Critical energy: ℏω_c ≈ 3 γ² ℏω_β (r_β/λ_β).
Brightness comparable to 3rd-generation synchrotron but in fs bursts.

## Key LWFA Facilities

| Facility | P (TW) | λ (μm) | τ (fs) | E_pulse (J) | Stage |
|----------|--------|--------|--------|-------------|-------|
| BELLA (LBNL) | 300 | 0.8 | 30 | 9 | 1 (8 GeV) |
| SULF (Shanghai) | 500 | 0.8 | 30 | 15 | 1 |
| Astra-Gemini (RAL) | 500 | 0.8 | 40 | 20 | 1 |
| HZDR Draco | 150 | 0.8 | 30 | 4.5 | 1 (5 GeV) |
| APOLLON (France) | 3000 | 0.8 | 15 | 150 | 1 (planned) |
| ELI-Beamlines | 10000 | 0.8 | 20 | 200 | 1 (10+ GeV) |

## Staging and Multi-GeV

Staging concept: multiple LWFA stages in series, each boosting energy.
Required: ~μm alignment precision, temporal synchronization ~fs.
Key challenge: beam transport between stages (emittance preservation).
Record: 2-stage acceleration demonstrated (LBNL 2016, 5+1 GeV).

## Cross-References

- laser-plasma: reasoning.lp.laser_wakefield_acceleration (parent — theory)
- laser-plasma: reasoning.lp.direct_laser_acceleration (alternative mechanism)
- laser-plasma: knowledge.lp.plasma_parameters_laser (I↔a₀, n_c)
