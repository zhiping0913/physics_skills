---
skill_id: reasoning.lp.ponderomotive_force
type: reasoning
summary_50t: >
  Ponderomotive force f_p = −(e²/4m_eω²)∇|E|² expels electrons from
  high-intensity regions. Density profile: n_e = n₀ exp(−|E|²/E_p²) where
  E_p² = 4m_eω²T_e/e². Hole-boring: piston velocity v_p/c = √(Ξ/(1+Ξ)),
  Ξ = I/(ρc³). Applications: density steepening at critical surface,
  self-focusing precondition, ion acceleration (RPA). Cross-domain:
  same ∇|E|² structure as optical trapping of particles.
trigger:
  - computing density modification by intense laser fields
  - estimating hole-boring velocity through overdense plasma
  - understanding the driver of profile steepening and channel formation
reasoning_role: ponderomotive_force
parent: reasoning.lp.laser_propagation_plasma
retrieval_cost: 1
sign_convention: >
  Time-averaged over laser period. f_p = −∇Φ_p where Φ_p = (e²|E|²)/(4m_eω²)
  is the ponderomotive potential (in energy units). a₀ = e|E|/(m_eωc).
  Electrons expelled from high |E|²; ambipolar field pulls ions.
---

# reasoning.lp.ponderomotive_force — ∇|E|² → Density Modification

## Core Picture

The ponderomotive force is the time-averaged force that an inhomogeneous
electromagnetic field exerts on charged particles. It is conservative:
f_p = −∇Φ_p, where Φ_p = (e²/4m_e ω²)|E|² is the ponderomotive potential.
This force expels electrons from high-intensity regions, creating density
cavities, steepening the critical-surface profile, and ultimately boring
a channel through overdense plasma. It is the plasma analog of optical
trapping (dielectric particles in laser tweezers) and the fundamental
driver of radiation-pressure ion acceleration (Kruer §5, Gibbon §5,
Macchi §5).

## Derivation Sketch

### 1. Equation of motion with oscillatory field

Electron momentum equation:
```
m_e dv/dt = −e(E + v×B)
```
For E = E₀(r) cos ωt (spatially non-uniform amplitude):
```
v = v_os + v_d    where v_os = −(e/m_eω) E₀(r) sin ωt [fast quiver]
```
Time-average ⟨v_os·∇⟩v_os over one laser period yields:
```
m_e⟨dv/dt⟩ = −(e²/4m_eω²) ∇|E₀|² ≡ −∇Φ_p       (1.1)
```

### 2. Ponderomotive potential

```
Φ_p = (e²/4m_eω²) |E₀|² = ½ m_e c² a₀²
```
where a₀ = e|E₀|/m_eωc is the normalized vector potential.
For a₀ = 1 at 800 nm: Φ_p ≈ 255 keV. For a₀ = 10: Φ_p ≈ 2.55 MeV.

**Key**: the force is proportional to ∇|E|², not |E|². Only gradients in
intensity produce a net force. A uniform field gives zero ponderomotive
force.

### 3. Density profile modification

In equilibrium, the ponderomotive force balances the electron pressure
gradient:
```
n_e∇Φ_p = −T_e ∇n_e
→  n_e(r) = n₀ exp(−Φ_p(r)/T_e)
```
Electrons are expelled from high |E|² regions by Φ_p/T_e e-foldings.
For Φ_p ≪ T_e: weak expulsion. For Φ_p ≫ T_e: complete electron cavitation.

**Critical surface steepening**: The ponderomotive force pushes the
critical surface to higher density, steepening the profile:
```
L_n → L_n / (1 + Φ_p/T_e)    [effective density scale length shortened]
```

### 4. Hole boring (piston model)

At ultra-high intensities (a₀ ≫ 1, I > 10¹⁸ W/cm²), the radiation pressure
pushes the critical surface forward into overdense plasma as a piston:
```
P_rad = 2I/c · (1+R)/(1−R) ≈ 2I/c    [for high reflectivity R≈0.9]
```
Balancing against the momentum flux of ions swept up:
```
P_rad = 2 n_i m_i v_p²
→  v_p/c = √(I/(ρc³)) ≡ √Ξ    where Ξ = I/(ρc³)
```
More precisely (non-relativistic ions, relativistic electrons):
```
v_p/c = √(Ξ/(1+Ξ))    [hole-boring velocity]
```
For I=10²⁰ W/cm² on a gas jet (n_e=5×10¹⁹ cm⁻³ H₂, ρ≈1.7×10⁻⁴ g/cm³): Ξ ≈ 2.2, v_hb/c ≈ 0.83. For solid Al (ρ=2.7 g/cm³): Ξ ≈ 1.4×10⁻⁵, v_hb/c ≈ 0.004 — hole boring negligible at solid density for current lasers.

NOTE: For solid-density targets at I < 10²² W/cm², hole boring is negligible (Ξ ≪ 1, v_hb ≪ c). Significant hole boring (v_hb/c > 0.5) requires either gas-jet targets (low ρ) or I > 10²² W/cm² (solid targets).

Hole-boring depth during pulse τ_L:
```
d_hb ≈ v_p τ_L
```

### 5. Ponderomotive channeling

In underdense plasma (n_e < n_c), the ponderomotive force expels
electrons RADIALLY from the laser axis, creating a density channel:
```
n_e(r) = n₀ [1 + (a₀²/2)(w₀²/w²(r)) exp(−2r²/w²(r))]^{-1}
```
The density depletion on-axis reduces the local plasma frequency →
waveguide effect → relativistic self-focusing (see R9).

## Algorithm — Given (I, λ, n₀, T_e) → Density Modification

```
1. COMPUTE a₀ = 0.85 × 10⁻⁹ λ[μm] √(I[W/cm²]).

2. COMPUTE Φ_p = ½ m_e c² a₀².
   Compare with T_e: if Φ_p/T_e < 0.1, ponderomotive effects negligible.

3. DENSITY PROFILE: n_e = n₀ exp(−Φ_p/T_e) in quasi-static equilibrium.
   For Φ_p/T_e > 1: electron cavitation, ions pulled by ambipolar field.

4. HOLE-BORING (overdense): v_p = c √(Ξ/(1+Ξ)), Ξ = I/(ρc³).
   Check: hole-boring significant when v_p τ_L > λ (piston depth > wavelength).

5. CHANNELING (underdense): radial expulsion → waveguide formation.
   Channel depth: Δn_e/n₀ ≈ a₀²/(1+a₀²).
```

## Cross-Domain Analogy

| Domain | Force | Form | Application |
|--------|-------|------|-------------|
| **Laser-plasma** | f_p = −∇Φ_p | Φ_p ∝ I/ω² | Hole boring, channeling, RPA |
| **Optical trapping** | f ≈ −(α/2)∇|E|² | polarizability α | Optical tweezers |
| **Paul trap** | f = −∇Φ_eff | Φ_eff ∝ E_rf² | Ion trapping |
| **Plasma wakefield** | f_p = −∇Φ_wake | Φ_wake ∝ a₀² | Electron acceleration |

## Edge Cases

- **Relativistic corrections**: For a₀ ≫ 1: f_p = −m_e c² ∇γ with
  γ = √(1+a₀²/2) — the force saturates at relativistic intensities.
- **Ion motion**: At long pulse durations (τ_L > 2π/ω_pi), ions also
  respond via the ambipolar field → density cavitation deepens.
- **3D effects**: Finite spot size → radial ponderomotive force →
  filamentation instability when P > P_cr.

## Cross-References

- Kruer §5, Gibbon §5, Macchi §5
- laser-plasma: reasoning.lp.laser_propagation_plasma (parent — propagation context)
- laser-plasma: reasoning.lp.relativistic_self_focusing (channeling → self-focusing)
- laser-plasma: reasoning.lp.radiation_pressure_acceleration (RPA = steady-state ponderomotive)
- electrodynamics: reasoning.em.nonlinear_optical_response (Kerr → ponderomotive analogy)
