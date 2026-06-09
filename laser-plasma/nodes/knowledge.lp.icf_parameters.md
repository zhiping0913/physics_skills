---
skill_id: knowledge.lp.icf_parameters
type: knowledge
summary_50t: >
  ICF ignition data: Lawson criterion nTτ > 3×10¹⁵ keV·s/cm³ (DT).
  NIF ignition point design: 1.8 MJ laser → 300 eV T_r → ρR ~ 1.5 g/cm²,
  T_i ~ 4 keV, yield ~ 20 MJ. Gain G = yield/E_laser. Ignition metrics:
  ITFX (experimental ignition threshold factor), χ_no-burn vs χ_burn.
  Alpha heating: Q_α = E_α/E_ext > 1 for ignition.
trigger:
  - checking if given implosion parameters achieve ignition
  - looking up NIF/LMJ design parameters
parent: reasoning.lp.fast_ignition
retrieval_cost: 1
---

# knowledge.lp.icf_parameters — Ignition Data & Designs

## Lawson Criterion — DT Fusion

For DT fuel at temperature T (keV), self-sustaining burn requires:
```
n τ > 3×10¹⁵ T[keV] cm⁻³·s     [T in keV, minimum at ~15 keV]
n τ T > 3×10¹⁵ keV·s/cm³        [triple product form]
```

In areal density form (for ICF):
```
ρR > 0.3 g/cm²    at    T_i > 5 keV    [hot spot ignition]
ρR > 1.0 g/cm²    for robust ignition   [with alpha transport losses]
```

| Parameter | Ignition threshold | Record (NIF 2021) | Comment |
|-----------|-------------------|-------------------|---------|
| ρR (g/cm²) | > 0.3 | ~0.3–0.5 | Hot spot |
| T_i (keV) | > 5 | ~4–5 | Ion temperature |
| nτ (s/cm³) | > 10¹⁴ | ~10¹⁴ | DT density × confinement |
| Yield (MJ) | — | 1.35 (2021) | NIF record |
| Q_α (=E_α/E_ext) | > 1 | ~1.3 (2023) | Alpha heating |

**NIF 2023 milestone**: yield 3.8 MJ, Q_α ~ 1.8, ignition achieved.
Laser energy: 2.05 MJ. Gain G ≈ 1.9.

## NIF Ignition Point Design

| Parameter | Value | Notes |
|-----------|-------|-------|
| Hohlraum | Au/U, 1 cm length | Cylindrical |
| Wall material | Depleted U (DU) | Optimized albedo |
| Gas fill | He, 0.96 mg/cm³ | Stagnate wall plasma |
| Capsule | High-Density Carbon (HDC) | Diamond-like |
| DT ice layer | 65 μm thick | Inner surface |
| DT gas fill | 0.3 mg/cm³ | Central |
| LEH diameter | 3.1 mm (each end) | — |
| Laser energy | 1.8–2.1 MJ | 3ω (351 nm) |
| T_r (peak) | ~300 eV | Hohlraum radiation temp |
| Pulse shape | 4-shock, ~15 ns | High-foot or low-foot |
| Implosion velocity | ~370 km/s | DT shell |
| Convergence ratio | ~30–35 | r_initial / r_final |
| Symmetry | < 1% RMS | Required for ignition |

## Ignition Metrics

**ITFX** (Experimental Ignition Threshold Factor):
```
ITFX = (ρR)^{0.07} × (Yield/10¹⁶)^{0.4}
```
ITFX > 1 → ignition conditions met. NIF 2021: ITFX ~ 0.7.

**Alpha heating parameter Q_α**:
```
Q_α = E_α_deposited / E_hot_spot
```
where E_α_deposited = 0.2 × Yield × f_dep (alpha deposition fraction).
Q_α > 1 → alpha self-heating dominates → ignition.

| Q_α | Regime | Physics |
|-----|--------|---------|
| < 0.1 | No burn | Alpha heating negligible |
| 0.1–0.5 | Low burn | Marginal alpha heating |
| 0.5–1.0 | Burning plasma | Significant self-heating |
| > 1.0 | Ignition | Alpha-dominated, thermal runaway |
| > 10 | Robust ignition | Burn propagation |

## Gain Curves

Energy gain G = Yield / E_laser:
```
G(DT) ≈ 100 × (ρR) × (burn fraction)    [marginal ignition]
G ≈ 20–50 for hot-spot ignition at NIF scale
G → ∞ for propagating burn (high ρR)
```

**Burn fraction** (for DT at given ρR):
```
f_burn ≈ ρR / (ρR + 6)    [g/cm², approximate]
```
For ρR = 3 g/cm²: f_burn ≈ 33%.

## Fast Ignition Parameters

| Parameter | Value | Notes |
|-----------|-------|-------|
| Ignitor energy | 10–20 kJ | In 10 ps |
| Ignitor power | 1–2 PW | Ultra-intense |
| Hot electron T_hot | 1–5 MeV | Ponderomotive |
| Coupling efficiency | 20–30% | Laser → hot spot |
| Cone tip position | 50 μm from fuel | ~electron range |
| Required ρR | > 0.3 g/cm² | Compressed fuel |

## Cross-References

- laser-plasma: reasoning.lp.fast_ignition (parent — FI theory)
- laser-plasma: reasoning.lp.hohlraum_physics (indirect drive context)
- laser-plasma: reasoning.lp.shock_waves_plasma (shock timing)
- laser-plasma: knowledge.lp.lpi_facilities (NIF, LMJ parameters)
