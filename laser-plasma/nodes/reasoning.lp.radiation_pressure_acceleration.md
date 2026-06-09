---
skill_id: reasoning.lp.radiation_pressure_acceleration
type: reasoning
summary_50t: >
  RPA (light-sail): circularly polarized laser pulse pushes thin foil as
  a piston via steady radiation pressure P_rad = 2I/c (no oscillatory j×B
  heating). Hole-boring RPA: v_p/c = √(Ξ/(1+Ξ)), Ξ = I/(ρc³). Light-sail
  RPA: ultra-thin foil Δ ≪ λ, v(t) evolves → γ_f ∝ a₀² τ_L / (n_e d).
  Monochromatic energy spectrum (unlike TNSA exponential). Requires
  ultra-high contrast, CP laser, nm-thickness targets.
trigger:
  - comparing RPA vs TNSA for ion acceleration
  - computing light-sail velocity and efficiency
  - designing RPA experiments (target thickness, pulse requirements)
reasoning_role: radiation_pressure_acceleration
parent: reasoning.lp.ponderomotive_force
retrieval_cost: 1
sign_convention: >
  Radiation pressure P_rad = 2I/c for perfect reflection (R=1).
  Ξ = I/(ρc³) = normalized piston parameter.
  CP (circular polarization) → no j×B heating → steady force.
  Target mass per area σ = n_e m_i d. Optimum: a₀ ≈ σ/(n_c m_i λ).
---

# reasoning.lp.radiation_pressure_acceleration — Light-Sail → Monoenergetic Ions

## Core Picture

Radiation Pressure Acceleration (RPA) uses the steady radiation pressure
of an ultra-intense laser to push a thin foil like a light-sail. Unlike
TNSA (which relies on hot electron sheaths), RPA directly transfers laser
momentum to the entire foil, producing a monoenergetic ion spectrum —
the "holy grail" of laser-ion acceleration. The key technical requirement
is a CIRCULARLY polarized (CP) laser: CP eliminates the oscillatory j×B
force that generates hot electrons, allowing pure radiation pressure
acceleration (Macchi et al., PRL 2005; Esirkepov et al., PRL 2004).

## Derivation Sketch

### 1. Radiation pressure — continuous force

For a perfectly reflecting foil at normal incidence:
```
P_rad = 2I/c    [perfect reflector]
P_rad = (1+R) I/c    [for reflectivity R]
```

The steady force on a foil of areal mass density σ = ρ d = n_e m_i d:
```
a = P_rad / σ = 2I/(c n_e m_i d)
```

### 2. Hole-boring RPA (thick target limit)

When the laser drills into an effectively thick target (d ≫ a₀ c/ω_p),
the critical surface is pushed forward at the hole-boring velocity:
```
v_hb / c = √(Ξ/(1+Ξ))
Ξ = I / (ρ c³) = I / (n_i m_i c³)
```

Ions are reflected from the moving critical surface (piston) with energy:
```
ε_i = 2 m_i v_hb²    [lab frame energy of reflected ions]
```

For I = 10²¹ W/cm² on solid Al (n_i ≈ 6×10²² cm⁻³): Ξ ≈ 6.2 → v_hb/c ≈ 0.93.
Reflected ions: ε_i ≈ 2 m_i c² Ξ/(1+Ξ) ≈ 20 MeV/nucleon.

### 3. Light-sail RPA (ultra-thin target)

When the target is SO thin that the entire foil is accelerated as a
coherent object (d ≪ λ, areal density σ small enough to move before
any significant heating occurs):
```
dv/dt = (P_rad / σ) · (1−v/c)/(1+v/c)    [relativistic Doppler]
```

In the target rest frame, the reflected intensity is reduced by
(1−v/c)/(1+v/c). The equation of motion has an analytic solution:
```
γ(v) = (1+v/c)/(1−v/c) → γ(t) ≈ (3 P_rad t / σ c)^{1/3} + const
```

**Final energy** (after pulse duration τ_L):
```
γ_f − 1 ≈ 2 (I/c²) τ_L / σ    [non-relativistic limit]
ε_i[MeV/u] ≈ 2 × 10⁻⁴ I_20 τ_L[fs] / σ[μg/cm²]    [practical]
```

For I = 5×10²⁰ W/cm², τ_L = 50 fs, σ = 1 μg/cm²: ε_i ≈ 500 MeV/u.

### 4. Why circular polarization matters

LP (linear polarization): E oscillates → v×B force oscillates at 2ω →
electron heating → T_hot rises → TNSA dominates.

CP (circular polarization): ponderomotive force has zero oscillatory
component → no electron heating → pure steady radiation pressure.

The ratio of RPA to TNSA efficiency: for CP, η_RPA/η_TNSA ≳ 10 for
optimized parameters.

### 5. Target requirements

**Thickness**: the foil must be thinner than the hole-boring depth:
```
d < d_opt ≈ (a₀/π) (n_c/n_e) λ    [light-sail condition]
```
For n_e = 300 n_c (solid density), a₀ = 10: d_opt ≈ 8 nm.
This is sub-wavelength — requires nm-thickness foils (e.g., DLC, CNT).

**Contrast**: pre-pulse must be < 10⁻¹⁰ of main pulse to avoid destroying
the foil before the main pulse arrives (plasma mirror needed).

## Algorithm — Given (I, λ, τ_L, n_e, d, Z) → RPA Parameters

```
1. COMPUTE areal density: σ = n_e m_i d.

2. COMPUTE Ξ = I/(ρc³).
   If target is thick, hole-boring: v_hb = c √(Ξ/(1+Ξ)).

3. CHECK light-sail condition: d < (a₀/π)(n_c/n_e)λ.
   If met: γ_f ≈ 1 + 2(I/c²)τ_L/σ.

4. POLARIZATION: if LP → j×B heating → TNSA contamination.
   Need CP for pure RPA.

5. MINIMUM INTENSITY: P_rad > P_plasma (plasma expansion pressure).
   Threshold: I > 10¹⁹ W/cm² for solid density targets.
```

## RPA vs TNSA — Comparison

| Aspect | TNSA | RPA (hole-boring) | RPA (light-sail) |
|--------|------|-------------------|-----------------|
| Spectrum | Exponential (dN/dε∝e^{−ε/T}) | Monoenergetic | Monoenergetic |
| Efficiency | ~5–10% | ~10–20% | ~20–30% |
| Polarization | LP or CP | LP or CP | CP required |
| Foil thickness | ~μm | ~100 nm | ~10 nm |
| Contrast req. | Moderate | High | Ultra-high (~10⁻¹¹) |
| Energy scaling | ε ∝ I^{1/2} | ε ∝ I | ε ∝ I τ_L/σ |
| Maturity | Well-established | Demonstrated | Demonstrated (challenging) |

## Edge Cases

- **Rayleigh-Taylor instability**: during light-sail acceleration, the
  foil is subject to RT instability → foil breakup before reaching high
  energy. Mitigated by ultra-thin foils and short pulses.
- **Transverse non-uniformity**: Gaussian laser profile → central region
  accelerated faster → foil curvature → reduced collimation.
- **Electron recirculation**: in ultra-thin foils, electrons can recirculate
  → enhanced heating → transition from RPA to TNSA.

## Cross-References

- Macchi et al., PRL 94, 165003 (2005) — RPA theory
- Esirkepov et al., PRL 92, 175003 (2004) — light-sail concept
- Henig et al., PRL 103, 245003 (2009) — experimental demonstration
- laser-plasma: reasoning.lp.ponderomotive_force (parent — radiation pressure = steady ponderomotive)
- laser-plasma: reasoning.lp.tnsa_ion_acceleration (analogy — alternative ion acceleration)
- laser-plasma: knowledge.lp.ion_acceleration_scaling (experimental benchmarks)
