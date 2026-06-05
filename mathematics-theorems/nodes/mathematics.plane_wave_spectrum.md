---
skill_id: mathematics.plane_wave_spectrum
type: reasoning
summary_50t: >
  2D Fourier representation of EM fields: E(r) = ∬ A(k_x,k_y) e^{i(k_x x+k_y y+k_z z)} dk_x dk_y.
  Propagating (k_ρ≤k) and evanescent (k_ρ>k) spectra. Weyl identity:
  e^{ikR}/(4πR) = (i/8π²)∬ e^{i(k_x x+k_y y+k_z|z|)} dk_x dk_y/k_z.
  Angular spectrum of Gaussian beams. Far-field = FT of aperture field.
trigger:
  - representing fields as superposition of plane waves
  - relating near-field to far-field, aperture diffraction
  - constructing spectral dyadic Green's functions
reasoning_role: plane_wave_spectrum
parent: mathematics.fourier_transform
retrieval_cost: 1
---

# mathematics.plane_wave_spectrum — Field → Angular Spectrum A(k_x,k_y)

## Core Picture

Any time-harmonic field in a source-free half-space z ≥ 0 can be represented
as a superposition of plane waves — both propagating (homogeneous, k_z real)
and evanescent (inhomogeneous, k_z imaginary). The complex amplitude A(k_x,k_y)
is the PLANE WAVE SPECTRUM (Clemmow 1996, Hansen & Yaghjian 1999).

## Derivation Sketch

Starting from `mathematics-theorems: mathematics.fourier_transform`:

### 1. 2D Fourier Representation in the z=0 plane

For a field E(x,y,0) known on z=0, the 2D Fourier transform:
```
A(k_x, k_y) = (1/4π²) ∬ E(x,y,0) e^{−i(k_x x + k_y y)} dx dy
```
The field at any z ≥ 0 (source-free, outgoing):
```
E(x,y,z) = ∬ A(k_x,k_y) e^{i(k_x x + k_y y + k_z z)} dk_x dk_y
```
where k_z = √(k² − k_x² − k_y²) = √(k² − k_ρ²) with k = ω/c.

### 2. Propagating vs. Evanescent Spectrum

```
k_ρ ≤ k:  k_z = +√(k²−k_ρ²)  REAL → propagating plane waves. Each (k_x,k_y)
          contributes a homogeneous plane wave with direction angles:
          sin θ = k_ρ/k, cos θ = k_z/k. The spectrum maps to far-field
          radiation pattern: E_ff(θ,φ) ∝ A(k sin θ cos φ, k sin θ sin φ).

k_ρ > k:  k_z = +i√(k_ρ²−k²) IMAGINARY → evanescent waves.
          Decay ∝ e^{−√(k_ρ²−k²)z}. Store sub-wavelength information.
          These are lost in the far field (only k_ρ≤k contributes).
```

### 3. Weyl Identity

The scalar spherical wave e^{ikR}/R as a plane wave superposition:
```
e^{ik|r−r'|}/(4π|r−r'|) = (i/8π²) ∬ e^{i[k_x(x−x')+k_y(y−y')+k_z|z−z'|]} dk_x dk_y/k_z
```
This is the 2D Fourier representation of the free-space Green's function.
It decomposes a spherical wave into plane waves — essential for layered
media Green's functions (Chew §2) and diffraction theory.

### 4. Angular Spectrum of Beams

For a Gaussian beam waist at z=0: E(x,y,0) = E₀ e^{−(x²+y²)/w₀²}
```
A(k_x,k_y) = (E₀ w₀²/4π) e^{−w₀²(k_x²+k_y²)/4}
```
The angular spread: Δθ ≈ λ/(πw₀). Narrow waist → broad angular spectrum.

## Algorithm

```
1. Known field on aperture plane (z=0): E_a(x,y,0).
2. Compute angular spectrum: A(k_x,k_y) = (1/4π²)∬ E_a e^{−ik_x x−ik_y y}dx dy.
3. Propagate to any z ≥ 0: multiply by e^{i k_z z}.
4. Far-field (z→∞): stationary phase evaluation → E(θ,φ) ∝ A(k_x,k_y)·(polarization).
5. Inverse: field at any (x,y,z) = ∬ A e^{i(k_x x + k_y y + k_z z)} dk_x dk_y.
```

## Applications

| Application | How PWS is used |
|-------------|-----------------|
| Near-field far-field transform (NFFFT) | Measured near-field → A → far-field pattern |
| Layered media Green's functions | Each plane wave independently reflects/transmits |
| Aperture diffraction | Kirchhoff integral = PWS of the aperture field |
| Gaussian beam propagation | A(k_x,k_y) is narrow Gaussian → beam stays collimated |

## Edge Cases

- **Evanescent wave recovery**: Super-resolution imaging requires recovering
  the evanescent spectrum (k_ρ>k). Near-field scanning optical microscopy
  (NSOM) achieves this with sub-wavelength probes.
- **Vector nature**: For EM fields, the spectrum must satisfy k·A = 0
  (divergence-free in source-free region). TE and TM decomposition in the
  spectral domain: A = A_TE (ê_TE) + A_TM (ê_TM).

## Cross-References

- Clemmow, *The Plane Wave Spectrum Representation of EM Fields* (1996)
- Hansen & Yaghjian, *Plane-Wave Theory of Time-Domain Fields* (1999)
- Chew, *Waves and Fields in Inhomogeneous Media* (1999) Ch.2
- mathematics-theorems: mathematics.fourier_transform (parent)
- mathematics-theorems: mathematics.sommerfeld_integral (Weyl identity = Sommerfeld identity)
- electrodynamics: reasoning.em.scalar_diffraction_kirchhoff (Fraunhofer = FT of aperture)
