---
skill_id: knowledge.lp.parametric_instability_data
type: knowledge
summary_50t: >
  SRS/SBS/TPD numerical data: growth rates, thresholds, convective
  gain exponents, experimental benchmarks. SRS threshold: Iλ² > 10¹⁴
  W·μm²/cm² for long L_n. SBS: lower threshold but saturates via
  ion trapping. TPD: n_c/4, γ₀/ω₀ ≈ 10⁻³ to 10⁻². ICF vulnerability.
trigger:
  - checking if given laser parameters exceed SRS/SBS threshold
  - computing convective gain for specific ICF plasma conditions
  - understanding backscatter fractions in NIF/OMEGA experiments
parent: reasoning.lp.parametric_instabilities_lpi
retrieval_cost: 1
---

# knowledge.lp.parametric_instability_data — Thresholds & Benchmarks

## SRS — Thresholds and Growth Rates

**Homogeneous growth** (backscatter, n_e ≪ n_c/4):
```
γ₀/ω₀ = (a₀/4) √(n_e/n_c)
```

| I (W/cm²) at 0.351μm | a₀ | n_e/n_c | γ₀/ω₀ | γ₀ (s⁻¹) |
|----------------------|-----|---------|--------|----------|
| 10¹⁴ | 0.0026 | 0.1 | 2.1×10⁻⁴ | 5.6×10¹¹ |
| 10¹⁵ | 0.0082 | 0.1 | 6.5×10⁻⁴ | 1.7×10¹² |
| 10¹⁶ | 0.026 | 0.1 | 2.1×10⁻³ | 5.6×10¹² |
| 10¹⁴ | 0.0026 | 0.2 | 2.9×10⁻⁴ | 7.8×10¹¹ |
| 10¹⁵ | 0.0082 | 0.2 | 9.2×10⁻⁴ | 2.5×10¹² |

**Convective threshold** (Rosenbluth gain):
```
G = 2π γ₀² L / (v_g1 v_g2 κ') > 10    [for observable SRS]
```
For ICF-relevant plasma (L ~ 1 mm, T_e ~ 3 keV, n_e ~ 0.1n_c):
threshold at I ~ 10¹⁴ W/cm².

**Absolute threshold** (at n_c/4):
```
(γ₀/ν_EPW)² > 1    [trapped-wave feedback condition]
```
Requires I > 10¹⁵ W/cm² at n_c/4 for typical ICF plasma.

## SBS — Thresholds and Growth Rates

```
γ₀/ω₀ = (a₀/4) √(n_e/n_c) (ω_p/ω_iaw) where ω_iaw = k_iaw c_s
```

| I (W/cm²) at 0.351μm | T_e (keV) | T_i (keV) | γ₀/ω₀ |
|----------------------|-----------|-----------|--------|
| 10¹⁴ | 3 | 1 | 5×10⁻⁵ |
| 10¹⁵ | 3 | 1 | 1.6×10⁻⁴ |
| 10¹⁵ | 5 | 2 | 1.1×10⁻⁴ |

SBS threshold LOWER than SRS because backscatter at all densities.
But: ion Landau damping is strong (ν_IAW ≫ ν_EPW typically), so the
NET gain often similar to SRS.

**SBS convective gain** (ICF: L~1mm, n_e~0.1n_c):
```
G_SBS ∼ G_SRS × (ω_p/ω_iaw) / (ν_IAW/ν_EPW)
```
Typically G_SBS ~ 5–15 for ICF → backscatter fractions 10–30%.

## TPD — Threshold at n_c/4

```
γ₀/ω₀ = k_epw v_osc / 4    [kT_e/m_ec² ≪ 1 limit]
γ₀/ω₀ ≈ (a₀/2√2) at n_c/4
```

| I (W/cm²) at 0.351μm | a₀ | γ₀/ω₀ | Threshold? |
|----------------------|-----|--------|-----------|
| 5×10¹⁴ | 0.0059 | 2.1×10⁻³ | No |
| 10¹⁵ | 0.0082 | 2.9×10⁻³ | Marginal |
| 5×10¹⁵ | 0.018 | 6.4×10⁻³ | Yes |
| 10¹⁶ | 0.026 | 9.2×10⁻³ | Yes |

**Absolute threshold**: γ₀ > ν_EPW → typically I ~ 5×10¹⁴ W/cm² for
ICF-relevant n_c/4 plasma (T_e ~ 2 keV, ν_EPW/ω₀ ~ 2×10⁻³).

**Hot electron temperature** from TPD:
```
T_hot ≈ 10–100 keV (depending on pump depletion and EPW amplitude)
```
This is the critical risk for ICF — hot electrons preheat the fuel
and prevent compression.

## ICF Backscatter Benchmarks

| Facility | λ (μm) | I (W/cm²) | SRS (%) | SBS (%) | Total loss (%) |
|----------|--------|-----------|---------|---------|----------------|
| OMEGA (direct) | 0.351 | 10¹⁵ | 2–5 | 5–15 | 10–20 |
| NIF (indirect) | 0.351 | 10¹⁵ | 1–3 | 3–10 | 5–15 |
| NIF (polar-drive) | 0.351 | 10¹⁵ | 3–8 | 10–20 | 15–30 |

**Mitigation strategies** (ICF):
1. **Smoothing by spectral dispersion (SSD)**: reduce coherence → reduce SBS.
2. **High-Z dopants**: increase inverse bremsstrahlung → raise T_e → stronger
   Landau damping of IAW → suppress SBS.
3. **Low density fill**: n_e ≪ 0.1n_c → SRS weak, SBS dominant but manageable.
4. **Wavelength choice**: shorter λ → higher n_c → collisional absorption
   dominates → SRS/SBS in collisional regime → suppressed.

## Regime Diagram — Iλ² vs T_e

```
T_e low (≪ 1keV)                   T_e mid (1–5 keV)          T_e high (≫ 5keV)
─────────────────────────────────────────────────────────────────────────────
Iλ² < 10¹⁴: IB dominant             IB dominant               IB dominant
Iλ² ~ 10¹⁴–10¹⁵: SRS suppressed     SRS + SBS grow           SRS/SBS/suppressed
  (collisional ν_ei)                 (ν_ei ≪ γ₀)
Iλ² > 10¹⁵: Brunel (steep)          SRS/SBS + Brunel          SRS still grows
                                       SRS absolute at n_c/4    (plasma hot)
```

**SBS vs SRS convective gain ratio**: 
G_SBS/G_SRS ≈ (v_g^EPW/v_g^IAW) × (γ₀^SBS/γ₀^SRS)².
Typically v_g^EPW/v_g^IAW ∼ 10–100 while γ₀^SBS/γ₀^SRS ∼ 0.01–0.1,
so G_SBS/G_SRS ∼ 0.1–10 — comparable despite lower SBS growth rate.

## Cross-References

- laser-plasma: reasoning.lp.parametric_instabilities_lpi (parent — theory)
- laser-plasma: knowledge.lp.plasma_parameters_laser (ν_ei, a₀ conversions)
- laser-plasma: reasoning.lp.laser_absorption_mechanisms (IB competes)
