---
skill_id: knowledge.lp.plasma_parameters_laser
type: knowledge
summary_50t: >
  Reference tables for laser-plasma parameter space. n_c(λ) =
  1.1×10²¹/λ²(μm) cm⁻³. a₀ = 0.85×10⁻⁹ λ(μm) √I(W/cm²).
  Convert between I, a₀, E(V/m), B(T). Relativistic threshold
  a₀=1 → I = 1.37×10¹⁸/λ²(μm) W/cm².
trigger:
  - converting between laser intensity and normalized amplitude
  - looking up critical densities for different laser wavelengths
  - computing electron quiver energy (ponderomotive potential)
parent: reasoning.lp.laser_propagation_plasma
retrieval_cost: 1
---

# knowledge.lp.plasma_parameters_laser — Unit Conversion Tables

## Critical Density by Wavelength

| Laser System | λ (nm) | n_c (cm⁻³) | ℏω (eV) |
|-------------|--------|-----------|--------|
| CO₂ | 10600 | 9.8 × 10¹⁸ | 0.117 |
| Er:fiber | 1550 | 4.6 × 10²⁰ | 0.80 |
| Nd:glass (1ω) | 1053 | 1.0 × 10²¹ | 1.18 |
| Nd:glass (2ω) | 527 | 4.0 × 10²¹ | 2.35 |
| Ti:sapphire | 800 | 1.7 × 10²¹ | 1.55 |
| Nd:glass (3ω) | 351 | 9.0 × 10²¹ | 3.53 |
| KrF | 248 | 1.8 × 10²² | 5.00 |
| Nd:glass (4ω) | 263 | 1.6 × 10²² | 4.71 |
| ArF | 193 | 2.9 × 10²² | 6.42 |
| XFEL (soft x-ray) | 1.0 | 1.1 × 10²⁷ | 1240 |

Formula: n_c[cm⁻³] = 1.1148 × 10²¹ / λ²[μm]

## Intensity ↔ Normalized Amplitude Conversion

```
a₀ = e|E|/(m_e ω c) = 0.855 × 10⁻⁹ λ[μm] √(I[W/cm²])
```

| I (W/cm²) | a₀ at 1 μm | a₀ at 0.8 μm | a₀ at 10.6 μm | Regime |
|-----------|------------|--------------|---------------|--------|
| 10¹² | 8.6×10⁻⁴ | 6.8×10⁻⁴ | 9.0×10⁻³ | Perturbative |
| 10¹⁴ | 8.6×10⁻³ | 6.8×10⁻³ | 9.0×10⁻² | Perturbative |
| 10¹⁶ | 8.6×10⁻² | 6.8×10⁻² | 0.90 | Weak relativistic |
| 10¹⁸ | 0.86 | 0.68 | 9.0 | Relativistic |
| 10²⁰ | 8.6 | 6.8 | 90 | Ultra-relativistic |
| 10²² | 86 | 68 | 900 | QED regime |

Relativistic threshold (a₀ = 1):
```
I_rel[W/cm²] = 1.37 × 10¹⁸ / λ²[μm]
```

## Ponderomotive Potential

```
Φ_p = m_e c² (γ−1) ≈ ½ m_e c² a₀²    [non-relativistic: a₀ ≪ 1]
Φ_p[eV] ≈ 255 × a₀²                    [for a₀ ≪ 1]
Φ_p[MeV] ≈ 0.511 × (√(1+a₀²/2) − 1)   [full relativistic]
```

| a₀ | Φ_p (non-rel) | Φ_p (relativistic) | I at 0.8 μm (W/cm²) |
|----|---------------|-------------------|---------------------|
| 0.1 | 2.55 keV | 2.55 keV | 2.1×10¹⁶ |
| 1.0 | 255 keV | 255 keV | 2.1×10¹⁸ |
| 5.0 | 6.38 MeV | 4.80 MeV | 5.3×10¹⁹ |
| 10 | 25.5 MeV | 13.0 MeV | 2.1×10²⁰ |
| 100 | 2.55 GeV | 195 MeV | 2.1×10²² |

## Electron Quiver Velocity and Energy

```
v_osc/c = a₀/√(1+a₀²/2)           [relativistic circular pol.]
v_osc/c = a₀                       [linear pol., non-rel only]
γ = √(1 + a₀²/2)                   [circular pol., pw]
γ = √(1 + a₀²)                     [linear pol., approximate]
```

## Field Strengths

```
E₀[V/m] = 3.21 × 10⁶ a₀ / λ[μm]
E₀[TV/m] = 3.21 × a₀ / λ[μm]
B₀[T] = a₀ / (94.2 λ[μm])
```

| a₀=1, λ=1μm | Value |
|-------------|-------|
| E₀ | 3.21 TV/m |
| B₀ | 10.6 kT |
| I | 1.37×10¹⁸ W/cm² |

## Plasma Frequency and Skin Depth

```
ω_p[rad/s] = 5.64 × 10⁴ √(n_e[cm⁻³])
f_p[Hz] = 8.98 × 10³ √(n_e[cm⁻³])
δ_skin = c/ω_p = 5.31 × 10⁵ / √(n_e[cm⁻³]) [cm]
```

| n_e (cm⁻³) | f_p (Hz) | δ_skin | Notes |
|------------|---------|--------|-------|
| 10¹⁹ | 2.84×10¹³ | 53 μm | CO₂ critical |
| 10²⁰ | 8.98×10¹³ | 17 μm | — |
| 10²¹ | 2.84×10¹⁴ | 5.3 μm | Near-IR critical |
| 10²² | 8.98×10¹⁴ | 1.7 μm | KrF critical |
| 10²³ | 2.84×10¹⁵ | 0.53 μm | Solid density |

## Collision Frequency

```
ν_ei[s⁻¹] = 3.0 × 10⁻⁶ n_e[cm⁻³] Z lnΛ / T_e^{3/2}[eV]
lnΛ ≈ 32 − ½ ln(n_e[cm⁻³]) + ln T_e[eV]    [T_e ≲ 100 eV]
lnΛ ≈ 24 − ln(√(n_e[cm⁻³])/T_e[eV])         [T_e ≳ 1 keV]
```

## Cross-References

- laser-plasma: reasoning.lp.laser_propagation_plasma (parent — derives these formulas)
- laser-plasma: reasoning.lp.laser_absorption_mechanisms (α_IB uses ν_ei, n_c)
- laser-plasma: reasoning.lp.ponderomotive_force (Φ_p table)
