---
skill_id: reasoning.lp.fast_ignition
type: reasoning
summary_50t: >
  Fast ignition: decouple compression from ignition. Laser-driven electron
  or ion beam heats compressed DT fuel to T > 5 keV at ρR > 0.3 g/cm².
  Cone-guided FI: gold cone maintains path for ignitor pulse. Hot electron
  transport governed by resistive B-fields and collimation. K_α imaging
  for source characterization. Ignition energy: E_ig ≈ 10–20 kJ in 10 ps.
  Status: demonstrated heating but not yet full ignition.
trigger:
  - computing ignition energy requirements
  - analyzing hot electron transport in compressed plasma
  - comparing fast ignition with central hot spot ignition
reasoning_role: fast_ignition
parent: reasoning.lp.laser_absorption_mechanisms
retrieval_cost: 1
sign_convention: >
  ρR = areal density (mass per unit area) in g/cm².
  Ignition condition: ρR T > 0.3 g/cm² at T > 5 keV.
  Hot electron divergence half-angle θ_div. K_α at 2.0 keV (cold) / 
  2.15 keV (warm) for Cu.
---

# reasoning.lp.fast_ignition — Decoupled Compression + Ignition

## Core Picture

Conventional inertial confinement fusion (ICF) compresses DT fuel to high
density AND heats it to ignition simultaneously via converging shocks
("central hot spot"). Fast ignition (FI) DECOUPLES these two steps:
(1) compress the fuel to high density (ρ > 300 g/cm³) via conventional
driver (NIF, LMJ), (2) ignite the compressed fuel with a separate,
ultra-intense, ultra-short laser pulse that generates a beam of relativistic
electrons or protons. This relaxes symmetry requirements and can potentially
achieve higher gain with less total driver energy (Tabak et al. 1994,
Atzeni §10-12, Kodama et al. 2001).

## Derivation Sketch

### 1. Ignition condition

The DT fuel must satisfy the Lawson-like criterion for alpha-particle
self-heating to sustain burn:
```
ρR > 0.3 g/cm²    at    T > 5 keV
```
where ρR is the areal density (mass per unit area). The alpha particles
(3.5 MeV from DT fusion) must deposit their energy within the hot spot.

**Hot spot size**: r_hs ≈ 20–30 μm, ρ ≈ 300 g/cm³ → ρR ≈ 0.6–0.9 g/cm².

**Ignition energy** (for a hot spot of mass M_hs):
```
E_ig ≈ 2 × (3/2) N k_B T ≈ 3 (M_hs/m_DT) k_B T
     ≈ 10–20 kJ for typical compressed DT parameters
```

This energy must be delivered in a time shorter than the hydrodynamic
disassembly time:
```
τ_dis ≈ r_hs / c_s ≈ 10–20 ps    [c_s ≈ 3×10⁷ cm/s at 5 keV]
```

Therefore: E_ig ≈ 10–20 kJ in ~10 ps → P_ig ≈ 1–2 PW.

### 2. Hot electron generation for FI

The ignitor laser (I ~ 10²⁰ W/cm², τ ~ 10 ps) interacts with the cone
tip or imploded plasma to generate relativistic electrons:
```
T_hot ≈ 0.5–5 MeV    [ponderomotive scaling at a₀ ~ 5–10]
η_L→e ≈ 20–40%        [laser-to-electron conversion efficiency]
```

The electron beam parameters:
```
I_e ≈ η_L→e I_L ≈ 10²⁰ W/cm²
ε_e ≈ T_hot ≈ 2 MeV    [typical electron energy]
n_e_bunch ≈ I_e/(T_hot c) ≈ 10²¹ cm⁻³
```

### 3. Electron transport — resistive collimation

Hot electrons propagate through the compressed plasma to the hot spot.
The transport is governed by:

- **Return current**: cold electron return current neutralizes the hot
  electron current to maintain ∇·J = 0. Resistive electric field E = η J_return.
- **Resistive magnetic field**: ∇×B = μ₀ J. The azimuthal B-field
  COLLIMATES the hot electron beam → reduced divergence.
- **Divergence**: θ_div ≈ 20–40° without collimation, 10–20° with strong
  resistive B-fields.

Transport distance from cone tip to hot spot: L_trans ≈ 50–100 μm.
This is comparable to the hot electron range at ρ ~ 300 g/cm³:
```
λ_e[μm] ≈ 0.5 (T_hot[MeV])² / (ρ[g/cm³] / 100)    [approximate]
```
For T_hot = 2 MeV, ρ = 300 g/cm³: λ_e ≈ 7 μm — electrons stop in ~7 μm.
This is the central challenge: hot electrons must be generated CLOSE to
the hot spot (cone-guided geometry required).

### 4. Cone-guided fast ignition

A gold cone is embedded in the fuel capsule:
- The cone maintains a vacuum (or low-density) path for the ignitor laser.
- The cone tip is positioned ~50 μm from the dense fuel.
- Protects the laser path from being blocked by the compressing plasma.

The cone-guided FI demonstrated at Gekko-XII / FIREX-I (Kodama 2001):
- 100× fuel heating observed (T increased from 0.3 to 1 keV).
- Coupling efficiency η_coupling ≈ 20–30%.
- Full ignition not yet achieved — requires higher energy and better coupling.

### 5. Proton fast ignition (alternative)

Instead of electrons, use laser-accelerated protons (TNSA):
- Protons have higher stopping power (Bragg peak) → more localized heating.
- Less sensitive to magnetic fields (higher rigidity).
- Requires proton generation close to fuel → additional target complexity.

## Algorithm — Given (ρ, ρR, T) → Ignition Requirements

```
1. CHECK ignition condition: ρR > 0.3 g/cm² at T > 5 keV.

2. COMPUTE hot spot mass: M_hs = (4π/3)ρ r_hs³.
   Energy required: E_ig ≈ 3 N k_B T.

3. ELECTRON BEAM REQUIREMENT:
   E_beam ≈ E_ig / η_coupling, η_coupling ≈ 0.2–0.5.
   Beam power: P_beam = E_beam / τ_dis ≈ 1–2 PW.

4. LASER REQUIREMENT:
   E_L ≈ E_beam / η_L→e, η_L→e ≈ 0.2–0.4.
   For E_ig = 15 kJ: E_L ≈ 80–150 kJ (delivered in 10 ps → 8–15 PW).

5. TRANSPORT: cone tip to hot spot distance < λ_e (electron range).
   At ρ > 300 g/cm³: cone tip within ~50 μm of hot spot.
```

## Edge Cases

- **Pre-pulse effects**: pre-pulse can preheat the cone tip plasma →
  laser absorption occurs before the critical surface reaches the hot spot
  → coupling efficiency drops.
- **Weibel instability**: counter-streaming hot and return electrons are
  Weibel-unstable → B-field filaments → enhanced divergence.
- **Alpha heating vs hot electron heating**: at full ignition, alpha
  self-heating dominates → hot electron source only needed as "spark plug".

## Cross-References

- Tabak et al., PoP 1, 1626 (1994) — fast ignition concept
- Kodama et al., Nature 2001 — first cone-guided FI experiment
- Atzeni §10-12, McKenna §8
- laser-plasma: reasoning.lp.laser_absorption_mechanisms (parent — hot electron generation)
- laser-plasma: reasoning.lp.tnsa_ion_acceleration (proton FI alternative)
- laser-plasma: reasoning.lp.hohlraum_physics (compression driver)
