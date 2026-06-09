---
skill_id: reasoning.lp.shock_waves_plasma
type: reasoning
summary_50t: >
  Plasma shocks: Rankine-Hugoniot conditions (mass, momentum, energy
  conservation across discontinuity). Shock adiabat (Hugoniot) vs
  isentrope. Strong shock limit: ρ₂/ρ₁ → (γ+1)/(γ-1). Radiation
  shocks (v > 50 km/s): radiation preheat precursor. Laser-driven
  shocks: ablative vs piston regime. Applications: ICF implosion,
  laboratory astrophysics, EOS measurement.
trigger:
  - computing post-shock density/temperature from laser drive
  - distinguishing radiation vs collisional shock regimes
  - analyzing shock timing in ICF implosions
reasoning_role: shock_waves
parent: reasoning.lp.laser_absorption_mechanisms
retrieval_cost: 1
sign_convention: >
  State 1 = upstream (unshocked). State 2 = downstream (shocked).
  Shock velocity D = v_shock in lab frame. u₁ = D, u₂ = particle
  velocity post-shock (in shock frame). Polytropic γ.
---

# reasoning.lp.shock_waves_plasma — Rankine-Hugoniot → Compressed State

## Core Picture

When a laser ablates a solid target, the recoil launches a shock wave
into the material. The shock is a thin (~collisional mean free path)
discontinuity where density, pressure, and temperature jump. The
Rankine-Hugoniot (RH) conditions relate the pre-shock and post-shock
states via conservation of mass, momentum, and energy across the
discontinuity. For laser-plasma interactions, shocks are fundamental
to ICF compression, equation-of-state (EOS) measurements, and laboratory
astrophysics (Zel'dovich & Raizer, Drake §4-5).

## Derivation Sketch

### 1. Rankine-Hugoniot conditions

In the shock rest frame (discontinuity stationary), conservation:
```
ρ₁ u₁ = ρ₂ u₂                         [mass]
ρ₁ u₁² + p₁ = ρ₂ u₂² + p₂             [momentum]
u₁²/2 + h₁ = u₂²/2 + h₂               [energy, h = ε + p/ρ]
```

where u₁ = D (shock velocity), u₂ is the post-shock particle velocity.

For an ideal gas (polytropic EOS: p = (γ−1)ρε):
```
ρ₂/ρ₁ = (γ+1)M² / ((γ−1)M² + 2)      [density compression]
p₂/p₁ = (2γM² − (γ−1)) / (γ+1)        [pressure jump]
```
where M = u₁/c_s1 is the shock Mach number.

### 2. Strong shock limit (M → ∞)

For M ≫ 1 (highly supersonic):
```
ρ₂/ρ₁ → (γ+1)/(γ−1)                   [maximum compression]
p₂/p₁ → (2γ/(γ+1)) M²
T₂ ∝ M²                                [post-shock temperature]
```

For monatomic gas (γ = 5/3): ρ₂/ρ₁ → 4 (maximum compression ratio).
For radiation-dominated gas (γ = 4/3): ρ₂/ρ₁ → 7.
With ionization/excitation (γ_eff < 5/3): higher compression possible.

### 3. Shock adiabat (Hugoniot) vs isentrope

The shock is inherently IRREVERSIBLE (entropy increase ΔS ∝ (Δp)³).
For a given compression ratio, the shock-heated pressure exceeds the
isentropic pressure:
```
p_Hugoniot > p_isentrope    [heating beyond adiabatic compression]
```

The Hugoniot curve in (p,V) space represents all possible shock
states for a given initial state. Crossing Hugoniots: when a second
shock or rarefaction reaches a shocked region.

### 4. Laser-driven shock regimes

**Ablative shock**: laser ablates material → recoil pressure launches shock.
```
p_ablation ≈ (I/10¹⁴)^{2/3} (λ/μm)^{-2/3} Mbar    [scaling]
```
For I = 10¹⁴ W/cm², λ = 0.35 μm: p_ablation ≈ 50 Mbar.

**Piston shock**: at very high intensity (a₀ ≫ 1), radiation pressure
acts as a direct piston. Hole-boring regime (RPA):
```
p_piston ≈ 2I/c ≈ 6.7 × I_20 Mbar
```

**Radiation shock**: at very high shock speeds (v_shock > 50 km/s for
low-Z, > 200 km/s for high-Z), the shocked material radiates strongly.
Radiation preheats the upstream → precursor → modified shock structure.

### 5. Shock timing in ICF

ICF implosion requires precise shock timing:
1. Initial weak shocks set the adiabat (entropy) of the fuel.
2. Main shock converges at the center → central hot spot.
3. Reflected shock from center → additional compression.
4. Timing precision required: ~50 ps for ignition.

The VISAR (Velocity Interferometer System for Any Reflector) diagnostic
measures shock velocity history → validates the RH model.

## Algorithm — Given (v_shock, ρ₁, material) → Post-Shock State

```
1. COMPUTE Mach number: M = v_shock / c_s1.
   c_s1 = √(γk_B T₁/m) for ideal gas.

2. APPLY RH conditions:
   ρ₂/ρ₁ = (γ+1)M² / ((γ−1)M² + 2)
   p₂ = p₁ (2γM² − (γ−1))/(γ+1)
   T₂ = p₂/(n₂ k_B)

3. STRONG SHOCK check: if M > 5, use asymptotic limits.

4. IONIZATION: T₂ > ionization threshold → γ_eff changes →
   iterate γ from EOS tables.

5. RADIATION: if T₂ > 100 eV, include radiation pressure and
   energy in RH conditions (modifies γ).
```

## Cross-References

- Zel'dovich & Raizer §1-7, Drake §4-5, Atzeni §3
- laser-plasma: reasoning.lp.laser_absorption_mechanisms (parent — ablation pressure)
- laser-plasma: reasoning.lp.hohlraum_physics (shock timing in indirect drive)
- laser-plasma: reasoning.lp.radiative_hydrodynamics (radiation shock coupling)
- laser-plasma: reasoning.lp.radiation_pressure_acceleration (piston shock limit)
