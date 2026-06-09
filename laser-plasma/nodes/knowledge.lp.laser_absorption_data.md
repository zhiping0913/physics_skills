---
skill_id: knowledge.lp.laser_absorption_data
type: knowledge
summary_50t: >
  Numerical absorption data for laser-plasma coupling. Inverse
  bremsstrahlung: α_IB(cm⁻¹), opacity tables. Resonance absorption
  f_A(θ, L_n/λ). Brunel: f_A(v_osc). j×B: f_A(a₀). Experimental
  benchmarks for regime boundaries. Iλ² phase diagram for absorption
  mechanism dominance.
trigger:
  - looking up absorption coefficients for specific plasma conditions
  - determining which absorption mechanism dominates for given I,λ,T_e
  - experimental benchmark values for laser absorption efficiency
parent: reasoning.lp.laser_absorption_mechanisms
retrieval_cost: 1
---

# knowledge.lp.laser_absorption_data — Absorption Coefficients & Benchmarks

## Inverse Bremsstrahlung — Spatial Absorption Coefficient

```
α_IB = (ν_ei/c) (n_e/n_c) / √(1 − n_e/n_c)    [cm⁻¹, propagating]
α_IB ≈ (ν_ei/c) (n_e/n_c)²                     [n_e ≪ n_c]
```

| Condition | α_IB (cm⁻¹) | 1/α_IB |
|-----------|-------------|--------|
| n_e=10²¹, T_e=100eV, Z=1 | 3.2 | 0.31 cm |
| n_e=10²¹, T_e=1keV, Z=1 | 0.010 | 100 cm |
| n_e=10²², T_e=1keV, Z=5 | 0.85 | 1.2 cm |
| n_e=10¹⁹, T_e=10eV, Z=5 | 45 | 0.022 cm |

Rule of thumb: α_IB ∝ n_e² Z / T_e^{3/2} λ².

## Resonance Absorption — Peak Values

Ginzburg function φ(τ) for linear density ramp:
```
τ = (ωL_n/c)^{1/3} sinθ
φ(τ) ≈ 2.3 τ exp(−2τ³/3)    [τ ≲ 1]
f_A ≈ ½ φ²(τ)
```

| L_n/λ | θ (°) | τ | φ(τ) | f_A |
|---------|-------|---|------|-----|
| 1 | 10 | 0.41 | 0.62 | 0.19 |
| 3 | 10 | 1.12 | 0.92 | 0.42 |
| 10 | 10 | 2.63 | 0.19 | 0.018 |
| 3 | 25 | 1.72 | 0.61 | 0.19 |
| 3 | 45 | 1.82 | 0.35 | 0.061 |
| 1 | 25 | 0.77 | 0.92 | 0.42 |

Optimum: τ ≈ 0.8 → f_A ≈ 0.5 for L_n/λ ≈ 1.5, θ ≈ 15°.

## Brunel Vacuum Heating — Formula Fit

```
f_A = (η/π) (v_osc/c)³    [Brunel 1987]
η ≈ 1.75 for an exponential density profile
```

| I (W/cm²) at λ=1μm | v_osc/c | f_A |
|--------------------|---------|-----|
| 10¹⁴ | 8.6×10⁻³ | 3.6×10⁻⁶ |
| 10¹⁶ | 8.6×10⁻² | 3.6×10⁻³ |
| 10¹⁷ | 0.27 | 0.11 |
| 10¹⁸ | 0.86 | 0.35 |

## j×B Heating — Scaling

```
f_A ≈ 0.5 a₀²/(1+a₀²) · (T_e/m_e c²)^{−1/2}    [approximately]
```

| a₀ | f_A (T_e=1keV) | f_A (T_e=100keV) |
|----|---------------|-----------------|
| 0.5 | 0.011 | 0.035 |
| 1.0 | 0.022 | 0.070 |
| 5.0 | 0.048 | 0.15 |
| 10 | 0.050 | 0.16 |

Note: j×B absorption generally < 20% even at a₀ ≫ 1. Other mechanisms
(ponderomotive steepening, vacuum heating) dominate at these intensities.

## Iλ² Phase Diagram — Absorption Mechanism Dominance

```
Iλ²[W·μm²/cm²]     Dominant Mechanism          f_A typical
──────────────────────────────────────────────────────────
< 10¹³              Inverse bremsstrahlung       0.1–0.8
10¹³ – 10¹⁵         Resonance absorption         0.1–0.5
10¹⁵ – 10¹⁷         Brunel vacuum heating        0.05–0.3
> 10¹⁷              j×B + ponderomotive          < 0.3
> 10²⁰              Hole boring → f_A → 1        up to 1
```

## Experimental Benchmarks

| Experiment | I (W/cm²) | λ (μm) | Mechanism | f_A measured | Notes |
|-----------|----------|--------|-----------|-------------|-------|
| ICF (OMEGA) | 10¹⁴ | 0.351 | Inverse bremsstrahlung | 0.80–0.95 | Long L_n, low Z |
| ICF (NIF) | 10¹⁵ | 0.351 | Collisional + resonance | 0.6–0.9 | Depends on θ |
| Solid target | 10¹⁷ | 0.8 | Brunel | 0.1–0.3 | Steep gradient |
| Foil target | 10²⁰ | 0.8 | Hole boring | 0.3–0.7 | a₀ > 3 |

Key: n_c for 4ω (263 nm) is much higher → absorption more collisional.
UV lasers favored for ICF direct-drive.

## Edge on Absorption Saturation

In ICF hohlraums, the intense x-ray radiation (~300 eV) pre-ionizes
the gas fill → L_n > 100s of μm → inverse bremsstrahlung dominates
completely at 0.351 μm. No resonance absorption or Brunel heating.
This is by design.

## Cross-References

- laser-plasma: reasoning.lp.laser_absorption_mechanisms (parent — theory)
- laser-plasma: knowledge.lp.plasma_parameters_laser (ν_ei, n_c, a₀ conversions)
