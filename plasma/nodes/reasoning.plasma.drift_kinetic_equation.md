---
skill_id: reasoning.plasma.drift_kinetic_equation
type: reasoning
summary_50t: >
  Gyroaveraging Vlasov: ∂⟨f⟩/∂t + v_∥ b̂·∇⟨f⟩ + v_d·∇⟨f⟩ = C[⟨f⟩].
  v_d = v_E + v_∇B + v_curv (electric, grad-B, curvature drifts). FLR
  corrections from Bessel J₀(k_⟂ρ). Banana orbits at trapped-passing boundary.
  Neoclassical: Pfirsch-Schlüter, plateau, banana regimes (ν_* = ν_eff/ω_b).
trigger:
  - inhomogeneous magnetized plasma with finite Larmor radius
  - neoclassical transport in tokamaks and stellarators
reasoning_role: drift_kinetic
parent: reasoning.plasma.kinetic_dielectric_response
retrieval_cost: 1
---

# reasoning.plasma.drift_kinetic_equation — Gyroaverage → FLR → Neoclassical

## Core Picture

In magnetized inhomogeneous plasma, the Vlasov equation with the full
6D phase space is computationally intractable. The drift-kinetic equation
(DKE) reduces the dimensionality by averaging over the fast gyromotion
(ω_c = qB/m is the fastest timescale), yielding an equation for the
guiding-center distribution ⟨f⟩(R, v_∥, v_⟂, t) where R is the guiding-
center position. The 5D DKE is the foundation of neoclassical transport
theory and gyrokinetic turbulence simulations.

## Derivation Sketch

### 1. Ordering and gyroaveraging

The fundamental ordering (Voprosy Vol.4, Volkov Ch.1): ω/ω_c ∼ ρ/L_n ∼ ϵ ≪ 1.
The particle position is r = R + ρ, where ρ = v_⟂/ω_c is the Larmor radius
vector. Expand f = f₀ + f₁ + ... and average over gyrophase φ:

```
⟨A⟩ = (1/2π) ∫₀^{2π} A(R + ρ(φ)) dφ    [gyroaverage]
```

The gyroaveraged Vlasov equation:

```
∂⟨f⟩/∂t + v_∥ b̂·∇⟨f⟩ + v_d·∇⟨f⟩ + a_∥ ∂⟨f⟩/∂v_∥ = C[⟨f⟩]
```

where v_d is the guiding-center drift velocity and a_∥ = (q/m) E_∥ − (μ/m) b̂·∇B
is the parallel acceleration with μ = mv_⟂²/(2B) the adiabatically invariant
magnetic moment.

### 2. Guiding-center drifts (from adiabatic theory)

The drift velocity v_d is the sum of contributions at different orders in ρ/L:

```
v_d = v_E + v_{∇B} + v_{curv} + v_{pol}
```

The individual drifts (from `landau-graph: reasoning.adiabatic_invariance` +
`plasma: knowledge.plasma.single_particle_drifts`):

| Drift | Velocity | Physics | Order |
|-------|----------|---------|-------|
| **E×B** | v_E = E×B/B² | Electric drift, independent of q,m | O(1) |
| **∇B** | v_{∇B} = (μ/q) B×∇B/B² | Magnetic moment seeks weak B | O(ϵ) |
| **Curvature** | v_{curv} = (mv_∥²/q) b̂×(b̂·∇)b̂/B | Centrifugal force on field line | O(ϵ) |
| **Polarization** | v_{pol} = (m/qB²) dE_⟂/dt | Inertial response to changing E | O(ϵ²) |

The grad-B and curvature drifts combine for vacuum magnetic fields
(∇×B = 0): v_{∇B} + v_{curv} = (m/qB³)(v_∥² + v_⟂²/2) B×∇B — the total
magnetic drift is proportional to the kinetic energy.

### 3. Finite Larmor radius (FLR) corrections

The gyroaverage of perturbed fields introduces Bessel functions. For
electrostatic perturbations φ̃ ∝ exp(ik·r):

```
⟨φ̃(R+ρ)⟩ = J₀(k_⟂ρ) φ̃(R)    [FLR: J₀ smoothing]
```

where J₀(z) ≈ 1 − z²/4 for z ≪ 1. FLR effects are crucial when k_⟂ρ ≳ 0.1:
they reduce the effective electric field experienced by the particle,
suppressing short-wavelength instabilities (FLR stabilisation of interchange
modes, drift waves). In the FLR expansion, the gyrokinetic equation replaces
the DKE when k_⟂ρ ∼ 1 — the full Bessel dependence is retained rather than
expanded (gyrokinetic ordering).

### 4. Neoclassical transport — three collisionality regimes

In toroidal geometry, trapped particles (banana orbits) and passing particles
respond differently to collisions. The dimensionless collisionality:

```
ν_* = ν_eff / ω_b = (ν R q) / (ϵ^{3/2} v_th)
```

where ν is the 90° deflection frequency, ω_b = ϵ^{1/2} v_th/(qR) is the bounce
frequency, and ϵ = r/R is the inverse aspect ratio.

The three regimes (Galeev & Sagdeev 1968):

| Regime | ν_* | Transport scaling | Physics |
|--------|-----|------------------|---------|
| **Banana** | ν_* ≪ 1 | D ∝ ν q² ϵ^{-3/2} ρ² | Trapped particles complete full banana orbits |
| **Plateau** | ν_* ∼ 1 | D ∝ q ϵ^{3/2} v_th ρ²/R (ν-independent) | Resonant detrapping |
| **Pfirsch-Schlüter** | ν_* ≫ 1 | D ∝ ν^{-1} q² ρ² (decreases with ν) | Collisional, MHD-like |

The banana regime enhancement factor over Pfirsch-Schlüter is ∝ ϵ^{-3/2} ∼ 30
for typical tokamaks (ϵ = 0.1) — trapped particles dominate the radial
transport. This is the physics behind the bootstrap current: the pressure
gradient drives a toroidal current in the banana regime with no external
loop voltage, scaling as j_bs ∝ (ϵ^{1/2}/B_θ) dp/dr.

## Algorithm — Given (equilibrium B(r), n(r), T(r)) → transport regime

```
1. Compute ρ_i = (2m_i kT)^{1/2}/(eB), ϵ = r/R, q(r)
2. ν_90 = n e⁴ lnΛ / (4π ε₀² m² v_th³) [Spitzer collision frequency]
3. Bounce frequency: ω_b = ϵ^{1/2} v_th/(qR)
4. ν_* = ν_90/(ϵ ω_b) → identify banana/plateau/Pfirsch-Schlüter
5. For banana regime: D ∝ q² ϵ^{-3/2} ρ² ν
6. For plateau: D ∝ q ϵ^{3/2} v_th ρ²/R (collisionless residual)
7. Bootstrap current: j_bs = −(ϵ^{1/2}/B_θ) (dp/dr) f_t (f_t ≈ 1.46 ϵ^{1/2})
```

## Edge Cases

- **Superbanana orbits**: when the rotational transform is very small (stellarator
  with ι ≪ 1/N), particles can be trapped in local magnetic wells within a
  single field period → transport scaling changes to D ∝ ν^{1/2}.
- **Electric field effects**: a radial electric field E_r creates an E×B poloidal
  rotation that can quench the banana regime when v_E×B > v_th ρ/R.
- **Gyrokinetic transition**: when k_⟂ρ ∼ 1, the DKE is replaced by the
  nonlinear gyrokinetic equation (Frieman-Chen 1982, modern codes: GENE, GYRO).

## Cross-References

- Voprosy Teorii Plazmy Vol.4 (1964), Volkov Ch.1: drift approximation
- Galeev & Sagdeev, *ZhETF* 53, 348 (1967) — neoclassical theory
- plasma: reasoning.plasma.single_particle_drifts (parent — individual drifts)
- plasma: reasoning.plasma.instability_classification (drift instabilities)
- landau-graph: reasoning.adiabatic_invariance (μ conservation → drifts)
