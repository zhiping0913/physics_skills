---
skill_id: reasoning.em.intensity_dependent_refractive_index
type: reasoning
summary_50t: >
  Intensity-dependent refractive index: N(I) = N₀ + N₂ I (Kerr) or
  N(a₀) = √(1−ω_p²/(γ(a₀)ω²)) (relativistic plasma). Common structure:
  on-axis intensity → Δn(I) → wavefront curvature → nonlinear lens.
  Critical power for self-focusing: P_cr ∝ λ²/(N₀ N₂). Shared
  mathematical skeleton across Kerr media, relativistic plasma,
  thermal lensing, photorefractive media.
trigger:
  - recognizing self-focusing in any physical domain
  - computing critical power from nonlinear index
  - abstracting the nonlinear lens formation mechanism
reasoning_role: nonlinear_index
parent: reasoning.em.nonlinear_optical_response
retrieval_cost: 1
sign_convention: >
  N = n + iκ (complex refractive index). N₂ in m²/W (Kerr).
  P_cr = critical power. Δφ_NL = nonlinear phase shift.
---

# reasoning.em.intensity_dependent_refractive_index — Δn(I) → Nonlinear Lens

## Core Picture

Many physical systems exhibit an intensity-dependent refractive index:
N(r) = N₀ + Δn(I(r)). For a beam with Gaussian intensity profile I(r) =
I₀ exp(−2r²/w²), the on-axis region experiences a different refractive
index than the wings. If Δn > 0 (self-focusing), the medium acts as a
positive lens. If Δn < 0 (self-defocusing), it acts as a negative lens.
When the nonlinear focusing overcomes diffraction, the beam collapses —
a universal phenomenon governed by the critical power P_cr.

This node captures the SHARED mathematical skeleton. Domain-specific
nodes provide the physical mechanism for Δn(I).

## Derivation Sketch

### 1. Nonlinear phase and lensing

For a beam propagating through a medium of thickness L:
```
φ(r) = (2π/λ) ∫₀^L N(r,z) dz
     = φ_linear + (2π/λ) ∫₀^L Δn(I(r,z)) dz
```

The radial phase curvature ∂²φ/∂r² determines whether the beam focuses
(negative curvature) or defocuses (positive curvature, in the e^{−iφ}
convention). For Δn = N₂ I with I = I₀ exp(−2r²/w²):
```
φ_NL(r) ≈ (2π/λ) N₂ I₀ L × (1 − 2r²/w²)
```
The r² term creates a lens of focal length f_NL ∝ w²/(N₂ I₀ L).

### 2. Critical power for self-focusing

Balancing nonlinear focusing against diffraction:
```
P_cr = α λ² / (4π N₀ N₂)    [Kerr media]
```
where α ≈ 1.86 for a Gaussian beam in bulk medium.

In a plasma waveguide (ponderomotive + relativistic):
```
P_cr ≈ 17 (n_c/n_e) GW      [relativistic plasma, z-dependent focusing]
```
The prefactor depends on geometry (bulk vs waveguide, CW vs pulsed).

### 3. Self-focusing length

For P > P_cr, the beam collapses over a distance:
```
Z_sf ≈ Z_R / √(P/P_cr − 1)    [Marburger 1975]
```
where Z_R = πw₀²/λ is the Rayleigh length. For P ≫ P_cr, Z_sf ≪ Z_R —
the beam self-focuses within a fraction of its diffraction length.

### 4. Filamentation instability (transverse)

A plane wave (or large-diameter beam) with intensity I₀ is unstable to
transverse modulations with spatial frequency k_⟂:
```
Γ_max ∝ (Δn(I₀)/N₀) ω     [growth rate]
k_⟂,opt ∝ √(Δn/N₀) / λ     [most unstable scale]
```
The beam breaks into filaments of width ~λ/√(Δn/N₀), each carrying ~P_cr.

### 5. Saturation mechanisms

| Mechanism | What limits | When |
|-----------|------------|------|
| Plasma defocusing (ponderomotive expulsion) | Relativistic focusing | n_e → 0 on axis |
| Multiphoton ionization | Kerr focusing in gases | Intensity > I_threshold |
| Material damage | Kerr focusing in solids | P > P_damage |
| Higher-order nonlinearities | Δn expansion | Δn ~ N₀ |
| Saturation of γ(a₀) | Plasma | a₀ ≫ 1 → Δn → ω_p²/2ω² |

## Domain-Specific Specializations

| Domain | N₀ | Δn(I) | P_cr | Node |
|--------|-----|-------|------|------|
| Kerr (fused silica) | 1.45 | n₂ I (n₂≈3×10⁻²⁰ m²/W) | ~4 MW at 1 μm | uo.NLSE |
| Relativistic plasma | √(1−ω_p²/ω²) | ω_p²(1−1/γ)/2ω² | 17 n_c/n_e GW | lp.R9 |
| Ponderomotive plasma | √(1−ω_p²/ω²) | (ω_p²/ω²)(δn_e/n_e) | — | lp.R3 |
| Thermal lensing | N₀ | (dn/dT)ΔT(I) | — | — |
| Photorefractive | N₀ | Δn_photo ∝ E_space_charge | — | — |

## Algorithm — Given (N₀, Δn(I), λ, w₀) → Focusing Behavior

```
1. COMPUTE P_cr from medium parameters:
   Kerr: P_cr ≈ α λ²/(4π N₀ N₂)
   Plasma: P_cr ≈ 17 n_c/n_e GW

2. COMPUTE beam power P = πw₀²I₀/2.

3. IF P > P_cr: self-focusing.
   Z_sf ≈ Z_R / √(P/P_cr − 1).

4. FILAMENTATION: if w₀ > λ_p (plasma) or w₀ > λ/√(Δn/N₀),
   beam breaks into multiple filaments.

5. SATURATION: check which mechanism limits focusing at given I₀.
```

## Edge Cases

- **Pulsed vs CW**: for pulses shorter than the medium response time
  (τ_p < T_relaxation), the nonlinear index is time-dependent →
  moving focus, pulse splitting.
- **Non-instantaneous nonlinearity**: molecular reorientation (τ ~ ps),
  thermal (τ ~ μs), photorefractive (τ ~ ms). CW or long-pulse only.
- **Vectorial effects**: polarization-dependent Δn in anisotropic media.

## Cross-References

- electrodynamics: reasoning.em.nonlinear_optical_response (parent — nonlinear susceptibility)
- laser-plasma: reasoning.lp.relativistic_self_focusing (plasma specialization — R9)
- laser-plasma: reasoning.lp.ponderomotive_force (ponderomotive channeling — R3)
- ultrafast-optics: reasoning.uo.pulse_propagation_nlse_higher_order (Kerr/fiber specialization)
