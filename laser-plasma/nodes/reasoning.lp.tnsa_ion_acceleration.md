---
skill_id: reasoning.lp.tnsa_ion_acceleration
type: reasoning
summary_50t: >
  Target Normal Sheath Acceleration: laser-heated electrons stream through
  thin foil → Debye sheath at rear surface → electrostatic field
  E_sh ≈ k_B T_hot / (e λ_D) ≳ TV/m. Ions accelerated to ε_max ∝ T_hot
  ln(ω_pi t). T_hot ∝ (Iλ²)^α, α ≈ 0.3–0.5. Quasi-neutral plasma
  expansion → exponential ion spectrum, dN/dε ∝ exp(−ε/T_hot).
  Applications: proton radiography, fast ignition.
trigger:
  - computing maximum ion energy from laser and target parameters
  - designing TNSA experiments (foil thickness, intensity)
  - understanding ion spectrum shape from sheath expansion
reasoning_role: tnsa_ion_acceleration
parent: reasoning.lp.laser_absorption_mechanisms
retrieval_cost: 1
sign_convention: >
  Target rear surface at z=0. Ions accelerated in +z (laser direction).
  Sheath field E_sh at rear surface. T_hot = hot electron temperature.
  ε_max = maximum ion kinetic energy. λ_D = Debye length.
---

# reasoning.lp.tnsa_ion_acceleration — Hot Electron Sheath → Ion Beam

## Core Picture

When an intense laser pulse irradiates a thin solid foil, it generates a
relativistic hot electron population (T_hot ≳ 100 keV–MeV) at the front
surface. These electrons propagate through the foil and exit the rear
surface, forming a dense electron cloud in vacuum. The electrostatic
field due to charge separation — the Debye sheath — accelerates ions
from the rear surface contaminant layer (typically protons from water
and hydrocarbons). This is Target Normal Sheath Acceleration (TNSA), the
most robust and widely studied laser-ion acceleration mechanism
(Snavely et al., PRL 2000; Wilks et al., PoFB 1992).

## Derivation Sketch

### 1. Hot electron generation

Laser absorption at the front surface via resonance absorption / Brunel /
j×B heating produces a hot electron population:
```
T_hot ≈ m_e c² (√(1+a₀²) − 1)   [ponderomotive scaling, Wilks 1992]
T_hot ≈ 3.6 (Iλ²/10¹⁴)^{0.42} keV    [Beg scaling, empirical fit]
T_hot ≈ 0.511 (γ₀ − 1) MeV           [relativistic]
```

For I = 10¹⁹ W/cm², λ = 1 μm: T_hot ≈ 0.5–2 MeV.

### 2. Electron propagation through foil

Hot electrons traverse the foil (thickness d), setting up a return current
in the cold electron background. The propagation is limited by:
- **Recirculation**: electrons reflect at rear sheath, return, reflect at
  front sheath → multiple passes → more uniform heating.
- **Foil thickness**: optimal thickness d_opt ≈ few × c/ω_p (∼1 μm for
  solid density) — thin enough to transmit electrons, thick enough to
  prevent pre-pulse damage.

### 3. Rear-surface sheath formation

At the rear surface, electrons escape into vacuum forming a cloud of
scale length ~λ_D:
```
λ_D = √(ε₀ k_B T_hot / n_e0 e²)    [Debye length]
n_e0 ≈ n_hot ≈ η E_abs / (T_hot V)  [hot electron density]
```

Quasi-static field: ∇p_e ≈ −e n_e E (pressure balance):
```
E_sh ≈ k_B T_hot / (e λ_D)
```

For T_hot = 1 MeV, n_hot = 10²⁰ cm⁻³: λ_D ≈ 0.7 μm, E_sh ≈ 1.4 TV/m.

### 4. Ion acceleration — quasi-neutral expansion

Ions in the surface contaminant layer (~nm thickness, mostly protons)
are accelerated by E_sh. The plasma expansion is described by the
self-similar isothermal model:
```
n_i(z,t) = n_i0 exp(−z/c_s t)    [Mora 2003]
E(z=0) = 2T_hot/(e c_s t)         [decaying sheath field]
```

The fastest ions reach velocity:
```
v_max(t) ≈ 2c_s ln(ω_pi t + √(1+ω_pi²t²))
ε_max ≈ 2 Z T_hot [ln(ω_pi τ_L) + ln 2 − 1]    [approximate]
```

where c_s = √(Z T_hot / m_i) is the ion sound speed and ω_pi is the
ion plasma frequency.

**Empirical scaling** (Fuchs 2006):
```
ε_max[MeV] ≈ 0.3 I_18^{0.5} λ_{μm}    [for thin foils, ~μm]
```
where I_18 = I/(10¹⁸ W/cm²).

### 5. Ion spectrum

The spectrum is exponential (not monoenergetic):
```
dN/dε ∝ exp(−ε/T_hot)    [quasi-thermal]
```
Cut-off at ε_max with typically 10⁸–10¹² protons per MeV at low energy.
The spectral shape limits applications requiring narrow energy spread.

## Algorithm — Given (I, λ, d_foil, τ_L) → TNSA Parameters

```
1. COMPUTE T_hot from laser parameters:
   a₀ = 0.85×10⁻⁹ λ[μm] √(I[W/cm²])
   T_hot ≈ m_e c² (√(1+a₀²)−1)

2. CHECK foil thickness: d_opt ≈ (5–10) × skin depth.
   Too thin → pre-pulse destroys foil. Too thick → electrons don't reach
   rear surface efficiently.

3. COMPUTE λ_D from T_hot and n_hot:
   n_hot ≈ η I / (T_hot c), η ≈ 0.1–0.3 (absorption efficiency)

4. SHEATH FIELD: E_sh ≈ T_hot / (e λ_D) ≈ √(n_hot T_hot/ε₀).

5. MAX ION ENERGY: ε_max ≈ 2 T_hot ln(ω_pi τ_L + 1).

6. SPECTRUM: dN/dε ∝ exp(−ε/T_hot), cutoff at ε_max.
```

## Edge Cases

- **Target pre-expansion**: pre-pulse (ns pedestal) can expand the rear
  surface before the main pulse → density gradient → reduced E_sh.
  Mitigation: plasma mirror for contrast enhancement.
- **Proton contamination**: protons (lowest Z/A) are preferentially
  accelerated because m_proton/Z = 1, while for C⁶⁺: m/Z = 2 →
  protons extracted first.
- **Limited acceleration length**: as the target expands, λ_D grows →
  E_sh drops → acceleration saturates after ~few ps.

## Cross-References

- Snavely et al., PRL 85, 2945 (2000) — first TNSA proton beam characterization
- Mora, PRL 90, 185002 (2003) — self-similar plasma expansion model
- Gibbon §7, Macchi §10
- laser-plasma: reasoning.lp.laser_absorption_mechanisms (parent — T_hot from absorption)
- laser-plasma: reasoning.lp.radiation_pressure_acceleration (analogy — alternative ion acceleration)
- laser-plasma: knowledge.lp.ion_acceleration_scaling (experimental benchmarks)
