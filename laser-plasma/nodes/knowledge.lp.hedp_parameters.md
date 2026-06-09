---
skill_id: knowledge.lp.hedp_parameters
type: knowledge
summary_50t: >
  High Energy Density Physics reference: HEDP regime (P > 1 Mbar,
  ε > 10¹¹ J/m³). EOS models: ideal gas, Thomas-Fermi, SESAME/QEOS
  tables. Shock Hugoniot data: U_s = C₀ + S u_p (linear fit). Radiation
  opacity regimes (Kramers, bound-free, lines). Warm dense matter
  (WDM): T ~ 1–100 eV, ρ ~ 0.1–10× solid, coupled/partially degenerate.
trigger:
  - looking up Hugoniot parameters for given material
  - determining if a state is in WDM regime
parent: reasoning.lp.shock_waves_plasma
retrieval_cost: 1
---

# knowledge.lp.hedp_parameters — HEDP Data & EOS

## HEDP Definition

| Parameter | Threshold | Notes |
|-----------|----------|-------|
| Pressure | P > 1 Mbar (10¹¹ Pa) | 1 Mbar = 100 GPa |
| Energy density | ε > 10¹¹ J/m³ | Chemical bond: ~10⁹ J/m³ |
| Temperature | T > 10 eV (1.2×10⁵ K) | Ionization threshold |
| Intensity | I > 10¹⁴ W/cm² (laser) | Ablation pressure > 1 Mbar |

Earth's core: P ≈ 3.6 Mbar, T ≈ 0.5 eV → *not* HEDP (too cold).
Sun's core: P ≈ 2×10¹¹ Mbar, T ≈ 1.3 keV → extreme HEDP.

## Shock Hugoniot — Linear Fit

For many materials, shock velocity U_s and particle velocity u_p:
```
U_s = C₀ + S u_p    [linear Hugoniot fit]
```

| Material | ρ₀ (g/cm³) | C₀ (km/s) | S | Notes |
|----------|------------|-----------|----|-------|
| Al | 2.70 | 5.33 | 1.34 | Standard reference |
| Cu | 8.93 | 3.94 | 1.49 | High-Z reference |
| Au | 19.3 | 3.06 | 1.55 | Hohlraum wall |
| Fe | 7.87 | 3.57 | 1.92 | Geophysical |
| Diamond (C) | 3.51 | 7.60 | 1.30 | High-T EOS |
| CH (plastic) | 1.04 | 2.82 | 1.46 | ICF ablator |
| Be | 1.85 | 8.00 | 1.20 | ICF ablator |
| DT (solid) | 0.25 | 2.30 | 1.55 | Fusion fuel |
| DT (gas) | 0.001 | 1.83 | 0.95 | — |
| H₂O | 1.00 | 1.65 | 1.92 | Equation of state |

Post-shock pressure from RH:
```
p = ρ₀ U_s u_p    [for strong shocks]
```

For U_s = 10 km/s, u_p = 5 km/s, Al (ρ₀=2.7): p ≈ 1.35 Mbar.

## EOS Models

| Model | Regime | Complexity | Notes |
|-------|--------|-----------|-------|
| Ideal gas | T ≫ T_F, non-degenerate | Low | p = nk_B T |
| Degenerate (Fermi) | T ≪ T_F | Low | p_F = (3π²)^{2/3}ℏ²n^{5/3}/5m |
| Thomas-Fermi | Intermediate | Medium | Semi-classical, Z-dependence |
| SESAME | Wide range | Table | LANL EOS library |
| QEOS | Wide range | Table | LLNL quotidian EOS |
| FEOS (Frankfurt) | Wide range | Table | Includes phase transitions |

**Fermi temperature**: T_F[eV] = (ℏ²/2m)(3π²n_e)^{2/3}.
For n_e = 10²³ cm⁻³ (solid): T_F ≈ 5 eV (partially degenerate at room T).

## Warm Dense Matter (WDM)

The regime between condensed matter and ideal plasma:
```
T: 0.1–100 eV (10³–10⁶ K)
ρ: 0.1–10× solid density (10²¹–10²⁴ cm⁻³)
Γ = e²/(a k_B T): 0.1–100 (coupling parameter)
Θ = T/T_F: 0.1–10 (degeneracy parameter)
```

WDM is challenging because:
- Neither condensed matter theory nor ideal plasma theory applies.
- Density functional theory + molecular dynamics (DFT-MD) required.
- X-ray Thomson scattering key diagnostic (measures S(k,ω)).

| Facility | WDM capability | Probe | Notes |
|----------|---------------|-------|-------|
| LCLS-MEC | XFEL + optical laser | X-ray | Warm dense Cu, Al |
| Omega | 60 beams, kJ | X-ray | Direct drive |
| NIF | 192 beams, MJ | X-ray | High-compression |
| PHELIX (GSI) | PW + ion beam | Proton | Heavy ion heating |

## Radiation Opacity Regimes

| Process | T range | κ ∝ | Dominant in |
|---------|---------|-----|------------|
| Free-free (Kramers) | > 100 eV | Z³ρ/T^{3.5} | Hohlraum interior |
| Bound-free | 10–500 eV | Complex Z-dependence | Wall plasma |
| Line opacity | 10–1000 eV | Many lines (~10⁶) | Rosseland mean |
| Electron scattering | > 10 keV | 0.2(1+X) cm²/g | High-T, constant |

**Opacity databases**: OPAL (LLNL), TOPS (LANL), STA (NRG).

## Cross-References

- laser-plasma: reasoning.lp.shock_waves_plasma (parent — Hugoniot)
- laser-plasma: reasoning.lp.radiative_hydrodynamics (opacity in transport)
- laser-plasma: reasoning.lp.hohlraum_physics (wall opacity)
