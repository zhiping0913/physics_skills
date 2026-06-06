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

Concrete procedure — plane wave spectrum computation, propagation, and field reconstruction:

```
INPUT:    Aperture field distribution E(x,y,0) on plane z=0.
          Wavenumber k = ω/c = 2π/λ.

STEP 1 — FOURIER TRANSFORM:
          A(k_x,k_y) = (1/4π²) ∬ E(x,y,0) e^{−i(k_x x + k_y y)} dx dy
          This is the plane wave spectrum (angular spectrum).

STEP 2 — CLASSIFY each spectral component:
          k_ρ = √(k_x² + k_y²)
          IF k_ρ ≤ k:  k_z = +√(k² − k_ρ²)       REAL → propagating (far-field)
          IF k_ρ > k:  k_z = +i√(k_ρ² − k²)      IMAGINARY → evanescent (near-field only)

STEP 3 — PROPAGATE to any z ≥ 0:
          Multiply each spectral component by the propagator e^{i k_z z}.
          A(k_x,k_y; z) = A(k_x,k_y) · e^{i k_z z}

STEP 4 — FAR-FIELD (Fraunhofer, z → ∞):
          Stationary phase evaluation collapses the inverse transform to
          E_ff(θ,φ) ∝ A(k sin θ cos φ, k sin θ sin φ)
          Only the k_ρ ≤ k (propagating) spectrum contributes.

STEP 5 — INVERSE (reconstruct field at any (x,y,z)):
          E(x,y,z) = ∬ A(k_x,k_y) e^{i(k_x x + k_y y + k_z z)} dk_x dk_y
          Numerical implementation: 2D IFFT of A(k_x,k_y; z).
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

## Cross-Domain Bridges

The plane wave spectrum connects into multiple domains — here is how it bridges:

| Domain | Bridge via PWS |
|--------|---------------|
| **Antenna NFFFT** | Near-field measurements → 2D FT → angular spectrum A(k_x,k_y) → far-field radiation pattern. Core of planar near-field far-field transform (NFFFT) scanners. |
| **Plasma** | In magnetized plasma, k_z depends on the anisotropic permittivity tensor ε̿. Each plane wave component sees a different refractive index depending on propagation direction relative to B₀ — PWS enables mode-by-mode field structure analysis. |
| **Optics** | Gaussian beam propagation: A(k_x,k_y) is itself a Gaussian → the beam remains Gaussian at all z (paraxial). A thin lens imparts a quadratic phase e^{−ik(x²+y²)/(2f)}, which in the spectrum domain is convolution — the lens acts as a Fourier transformer (Goodman, *Introduction to Fourier Optics*). |
| **SPP (Surface Plasmon Polariton)** | The evanescent spectrum (k_ρ > k) encodes sub-wavelength surface wave information. SPP dispersion lies beyond the light line — direct far-field observation is impossible; prism or grating coupling recovers the evanescent plane wave components. |

## Cross-References

- Clemmow, *The Plane Wave Spectrum Representation of EM Fields* (1996)
- Hansen & Yaghjian, *Plane-Wave Theory of Time-Domain Fields* (1999)
- Chew, *Waves and Fields in Inhomogeneous Media* (1999) Ch.2
- mathematics-theorems: mathematics.fourier_transform (parent)
- mathematics-theorems: mathematics.sommerfeld_integral (Weyl identity = Sommerfeld identity)
- electrodynamics: reasoning.em.scalar_diffraction_kirchhoff (Fraunhofer = FT of aperture)
