---
skill_id: mathematics.sommerfeld_integral
type: reasoning
summary_50t: >
  Sommerfeld identity: e^{ikR}/R = (i/2)∫₀^∞ H₀^(1)(k_ρ ρ) e^{ik_z|z|} (k_ρ/k_z) dk_ρ.
  Cylindrical wave → plane waves. Used for layered media dyadic Green's
  functions, branch cuts from k_z = √(k²−k_ρ²), surface wave poles,
  leaky wave poles. Riemann sheet selection per radiation condition.
trigger:
  - computing fields from sources in planar stratified media
  - constructing Green's functions for layered geometries
  - evaluating radiation from sources on or near interfaces
reasoning_role: sommerfeld_integral
parent: mathematics.plane_wave_spectrum
retrieval_cost: 1
---

# mathematics.sommerfeld_integral — 3D Wave → 1D k_ρ Integral

## Core Picture

A spherical wave e^{ikR}/R can be decomposed into cylindrical waves via the
Sommerfeld identity, reducing a 3D problem to a 1D integral over radial
wavenumber k_ρ (Sommerfeld 1909). This is the MATHEMATICAL ENGINE of layered
media Green's functions — each cylindrical wave component independently
interacts with planar interfaces.

## Derivation Sketch

Starting from `mathematics-theorems: mathematics.plane_wave_spectrum` (the
Weyl identity representing e^{ikR}/R as a 2D plane wave integral):

### 1. Sommerfeld Identity

Convert the Cartesian (k_x, k_y) integral to polar (k_ρ, α):
```
k_ρ² = k_x² + k_y²
∬ [...] dk_x dk_y = ∫₀^{2π} dα ∫₀^∞ dk_ρ k_ρ [...]
```
The angular integral yields the Bessel function J₀(k_ρ ρ). With the outgoing
Hankel function H₀^(1) = J₀ + iY₀ (proper for the radiation condition):
```
e^{ikR}/R = (i/2) ∫₀^∞ H₀^(1)(k_ρ ρ) e^{i k_z |z|} (k_ρ/k_z) dk_ρ
```
where k_z = √(k² − k_ρ²), ρ = √(x²+y²), R = √(ρ²+z²).

### 2. Branch Cuts and Riemann Sheets

k_z = √(k²−k_ρ²) is DOUBLE-VALUED in the complex k_ρ plane:
- **Top sheet** (physical): Im(k_z) ≥ 0 → waves decay or propagate outward.
- **Bottom sheet** (unphysical): Im(k_z) < 0 → waves grow at infinity.
Branch points at k_ρ = ±k. Branch cut connects them; standard choice is
the hyperbolic cut Im(k²−k_ρ²) = 0.

### 3. Singularities in the k_ρ Plane

```
Surface wave poles: k_z₁/k_z₂ = −ε₁/ε₂ (TM) or −μ₁/μ₂ (TE).
  → Real k_ρ > max(k₁,k₂) → Im(k_z₁,₂) > 0 → wave bound to interface.
  These are the discrete spectrum (guided modes).

Leaky wave poles: Complex k_ρ with Im(k_ρ) < 0, Im(k_z) < 0.
  → Initially on the bottom sheet; when the integration contour is
  deformed, these poles may be captured, contributing radiation at angles
  θ = sin⁻¹(Re(k_ρ)/k).

Branch cut integral: Continuous spectrum (radiation modes). Important
  for near-field and intermediate-zone calculations.
```

### 4. Application to Layered Media

In a planar stratified medium (e.g., substrate with ground plane), the
dyadic Green's function is expressed as a Sommerfeld integral:
```
G̿_e(r,r') = (i/8π²) ∬ A̿(k_ρ) e^{i k_ρ·(ρ−ρ')} e^{i k_z z} dk_x dk_y
```
For each k_ρ, the transmission-line analogy gives the reflection/transmission
coefficients → A̿(k_ρ). This is computationally the Method of Moments for
planar antennas and circuits (Okhmatovski & Zheng 2024).

## Algorithm

```
1. Express the desired field quantity as a Sommerfeld-type integral:
   f(ρ,z) = ∫₀^∞ F(k_ρ) J_n(k_ρ ρ) dk_ρ.

2. Analyze the integrand F(k_ρ) in the complex k_ρ plane:
   a. Locate branch points (±k_i for each layer) and poles.
   b. Determine the proper Riemann sheet for each k_z = √(k_i²−k_ρ²).

3. Deform the integration contour:
   a. Original: real axis 0→∞.
   b. Deform to steepest-descent path (SDP) through the saddle point.
   c. Capture any poles crossed during deformation → residue contributions.

4. Evaluate asymptotically (kρ ≫ 1): saddle point method (see
   mathematics.steepest_descent).

5. Numerically (general ρ): direct integration along real axis or SDP.
   Watch for oscillatory behavior when k_ρ ρ ≫ 1.
```

## Key Features

- **Transmission-line analogy**: In planar stratified media, the problem
  for each k_ρ reduces to a 1D transmission line with characteristic
  impedances Z_TE = ωμ/k_z, Z_TM = k_z/(ωε). Reflection/transmission
  coefficients follow the same formulas as voltage waves on lines.
- **Fresnel reflection coefficients naturally emerge** from matching
  the transmission-line impedances at each interface.

## Edge Cases

- **k_ρ ρ ≫ 1**: Integrand oscillates rapidly. Use asymptotic methods
  (steepest descent) or Filon integration. The saddle point k_ρ ≈ k sin θ
  gives the geometric-optics ray direction.
- **Source and observation on same interface (z=z'=0)**: The integral
  converges slowly. Extract the direct term (free-space G₀) analytically
  and integrate the reflected part numerically.
- **Lossy media (complex k)**: Branch points move off the real axis;
  contour deformation must track them.

## Cross-References

- Chew, *Waves and Fields in Inhomogeneous Media* (1999) Ch.2
- Okhmatovski & Zheng, *Theory and Computation of EM Fields in Layered Media* (2024)
- Felsen & Marcuvitz, *Radiation and Scattering of Waves* (1994) Ch.5
- mathematics-theorems: mathematics.plane_wave_spectrum (parent — Weyl identity)
- mathematics-theorems: mathematics.steepest_descent (asymptotic evaluation)
- electrodynamics: reasoning.em.dyadic_green_function (layered media G̿ via Sommerfeld)
