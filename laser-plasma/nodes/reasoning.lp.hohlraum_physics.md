---
skill_id: reasoning.lp.hohlraum_physics
type: reasoning
summary_50t: >
  Hohlraum: laser-irradiated high-Z cavity converts laser energy to X-rays
  (radiation temperature T_r ~ 300 eV). X-rays provide symmetric, indirect
  drive for ICF capsule implosion. Laser entrance hole (LEH) = loss channel.
  Wall losses ∝ T_r^{4.5}, X-ray conversion η_X ≈ 70–80%. Plasma filling
  from wall ablation restricts hohlraum lifetime. NIF: Au/U hohlraum,
  T_r ≈ 300 eV, E_laser ≈ 1.8 MJ.
trigger:
  - computing radiation temperature from hohlraum power balance
  - analyzing laser-plasma instabilities inside hohlraum
  - understanding indirect-drive ICF energy coupling
reasoning_role: hohlraum_physics
parent: reasoning.lp.laser_absorption_mechanisms
retrieval_cost: 1
sign_convention: >
  T_r = radiation temperature (eV or keV, typically 100–300 eV).
  T_r in eV: energy density U = a T_r⁴, a = 7.56×10⁻¹⁵ erg/cm³/eV⁴.
  X-ray conversion efficiency η_X = P_X / P_laser.
  Wall albedo α_w = re-emitted / absorbed.
---

# reasoning.lp.hohlraum_physics — Laser → X-rays → Implosion Drive

## Core Picture

In indirect-drive ICF, the laser beams do NOT directly irradiate the fusion
capsule. Instead, they enter a high-Z cavity (hohlraum, typically Au or U)
through laser entrance holes (LEHs), strike the inner wall, and are converted
to thermal X-rays. The X-ray radiation field (radiation temperature T_r ~ 300 eV)
provides a nearly uniform, symmetric drive that compresses the DT capsule.
NIF uses 192 beams delivering ~1.8 MJ of 3ω (351 nm) light to achieve T_r ~ 300 eV
in a cm-scale hohlraum (Lindl 1995, Atzeni §6-8, Rosen 1996).

## Derivation Sketch

### 1. Laser-to-X-ray conversion

Laser light is absorbed in the hohlraum wall plasma (typically at n_e ~ 10²¹ cm⁻³
for 3ω Nd:glass). The absorbed energy heats electrons, which radiate:
```
P_X = η_X P_abs    [X-ray power from absorbed laser]
η_X ≈ 0.7–0.8      [typical for Au at 3ω]
```

The X-ray spectrum is approximately Planckian at T_r:
```
I_ν = (2hν³/c²) / (e^{hν/k_B T_r} − 1)
Peak photon energy: hν_peak ≈ 2.82 k_B T_r ≈ 0.85 keV at T_r=300 eV
```

### 2. Power balance — determining T_r

In steady state, absorbed laser power = X-ray losses + wall losses:
```
P_abs = P_LEH + P_wall
```
where:
```
P_LEH = σ T_r⁴ A_LEH    [X-rays escaping through LEHs]
P_wall = (1−α_w) σ T_r⁴ A_wall    [net wall absorption]
```

Here σ = ac/4 = 1.03×10⁵ W/cm²/eV⁴ is the Stefan-Boltzmann constant in
practical units, and α_w is the wall albedo.

The radiation temperature is:
```
T_r⁴ = P_abs / [σ (A_LEH + (1−α_w) A_wall)]
```

For NIF-scale hohlraum (A_wall ~ 1 cm², A_LEH ~ 0.1 cm², α_w ~ 0.8–0.9):
```
T_r ≈ 300 eV at P_abs ≈ 500 TW (peak power)
```

### 3. Wall physics — albedo and loss

The X-ray albedo α_w depends on wall material and T_r:
```
α_w ≈ 1 − C / T_r^{0.5}    [approximately, for high-Z walls]
```
where C depends on the material opacity. Higher Z → higher opacity →
higher albedo → lower wall loss → higher T_r for the same laser power.

Wall materials:
- **Au** (gold): standard, α_w ≈ 0.8 at 300 eV. Well-characterized.
- **U** (depleted uranium): higher opacity → α_w ≈ 0.85–0.9 → higher
  T_r for same power. Used in NIF high-foot experiments.
- **Pb, W**: alternatives with different opacity characteristics.

### 4. Plasma filling — hohlraum lifetime

Laser heating ablates the inner wall, filling the hohlraum with plasma.
This plasma:
- **Absorbs/scatters laser light**: laser-plasma instabilities (SRS/SBS)
  in the hohlraum fill plasma → reduced coupling.
- **Blocks inner beams**: plasma fills the hohlraum, the laser path
  becomes opaque → "beam blocking."
- **Limits pulse duration**: typical hohlraum plasma filling time
  τ_fill ≈ 5–10 ns. The laser pulse must complete before filling.

Gas fill is typically introduced to control plasma expansion:
- He gas fill at ~1 mg/cm³ → stagnates wall blow-off → extends
  hohlraum lifetime.
- Trade-off: gas fill increases SRS/SBS risk (plasma at n_e ~ 0.1 n_c).

### 5. Drive symmetry — beam positioning

The X-ray radiation field must be symmetric on the capsule surface
(<1% RMS non-uniformity for ignition). Achieved via:
- **Multiple rings of beams**: NIF has 4 rings (23.5°, 30°, 44.5°, 50°).
- **Beam phasing**: temporal staggering of inner vs outer beams →
  dynamic symmetry control.
- **Hohlraum shape**: cylindrical with length-to-radius optimization.
- **Cross-beam energy transfer (CBET)**: controlled wavelength shift
  between beams → power redistribution → symmetry tuning.

### 6. Capsule coupling and hohlraum energetics

Energy flow in a NIF hohlraum:
```
Laser → X-rays:      η_X = 70–80%
X-rays → capsule:    η_cap ≈ 10–15% (geometric + albedo)
Capsule → fuel:      η_hydro ≈ 10–15%
Total:               η ≈ 0.7 × 0.12 × 0.12 ≈ 1%
```

For 1.8 MJ incident: ~18 kJ coupled to DT fuel. The fusion yield must
exceed the incident laser energy (gain > 1) for net energy production.

## Algorithm — Given (P_laser, hohlraum geometry) → T_r, coupling

```
1. COMPUTE wall area A_wall and LEH area A_LEH.

2. ESTIMATE wall albedo α_w for wall material at expected T_r.
   Au at 300 eV: α_w ≈ 0.8.
   U at 300 eV: α_w ≈ 0.88.

3. SOLVE power balance:
   T_r⁴ = η_X P_laser / [σ (A_LEH + (1−α_w) A_wall)]

   Iterate if α_w depends on T_r.

4. CHECK hohlraum filling: τ_pulse < τ_fill ≈ 5–10 ns.
   If τ_pulse > τ_fill → beam blocking → reduced coupling.

5. CAPSULE COUPLING:
   η_cap = (A_cap / A_wall) · α_w_effective
   P_cap = η_X η_cap P_laser.
```

## Edge Cases

- **Cross-beam energy transfer**: outer beams lose energy to inner beams
  via SBS in the flowing plasma → affects drive symmetry. Used as a
  tuning knob but can reduce total coupling.
- **Stimulated Brillouin scattering in gas**: He fill at ~1 mg/cm³ gives
  n_e ~ 10²⁰ cm⁻³ → SBS from f/8 beams at 3ω. Mitigated by SSD smoothing,
  but SBS backscatter can reach 10–20%.
- **Magnetic fields**: self-generated B-fields (~MG) in the hohlraum can
  affect electron thermal transport → hot spots on capsule.

## Cross-References

- Lindl, PoP 2, 3933 (1995) — indirect-drive ICF review
- Rosen, PoP 1996 — hohlraum physics model
- Atzeni §6-8, HPP-3 §6
- laser-plasma: reasoning.lp.laser_absorption_mechanisms (parent — absorption of laser in wall plasma)
- laser-plasma: reasoning.lp.parametric_instabilities_lpi (SRS/SBS in hohlraum fill)
- laser-plasma: reasoning.lp.fast_ignition (alternative ignition approach)
