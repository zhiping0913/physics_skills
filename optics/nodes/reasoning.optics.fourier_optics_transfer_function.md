---
skill_id: reasoning.optics.fourier_optics_transfer_function
type: reasoning
summary_50t: >
  Lens: front focal plane → back focal plane = Fourier transform. Coherent
  imaging: CTF H(f_x,f_y)=P(λz f_x,λz f_y), cutoff f_c=NA/λ. Incoherent:
  OTF=H★H, cutoff 2NA/λ. Resolution, apodization, phase contrast, holography.
trigger:
  - analyzing imaging system resolution and transfer functions
  - designing spatial filters, holographic systems
reasoning_role: fourier_optics
parent: reasoning.em.scattering_cross_section
retrieval_cost: 1
sign_convention: >
  FT pair: U(x) = ∫ u(f_x) exp(i2π f_x x) df_x, u(f_x) = ∫ U(x) exp(−i2π f_x x) dx.
  Time convention e^{−iωt} (Goodman §2). Spatial frequency f_x = x/λz = sin θ/λ.
  Positive f_x = wave vector component in +x. Phase factor exp(ikz) for +z propagation.
references:
  - electrodynamics: reasoning.em.scattering_cross_section (Fraunhofer diffraction)
---

# reasoning.optics.fourier_optics_transfer_function — Lens → FT → Image

## Core Picture

A lens performs a FOURIER TRANSFORM (Goodman §4-6). The field at the back
focal plane of a lens is the Fourier transform of the field at the front
focal plane. This transforms the problem of image formation from convolution
in real space to MULTIPLICATION in frequency space.

## Derivation Sketch

Starting from `electrodynamics: reasoning.em.scattering_cross_section`
(Fraunhofer diffraction = Fourier transform of aperture field, condition
N_F = a²/λz ≪ 1) and `knowledge.em.crystal_optics` (wave propagation in
anisotropic media — prerequisite for understanding pupil apodization and
polarization effects):

1. **Fraunhofer is the FT** (from scattering_cross_section):
   U(x,y) ∝ ∫∫ U_aperture(ξ,η) exp[−ik(xξ+yη)/z] dξdη
   = FT{U_aperture} evaluated at f_x = x/λz, f_y = y/λz.
   This is the critical bridge: the parent node establishes that far-field
   scattering IS a Fourier transform. Here we actively consume this result
   by placing a LENS to bring the far field to a finite distance.

2. **Lens as FT engine** (the key non-obvious step — Goodman §5.2):
   A lens of focal length f, placed with the object in its front focal plane,
   removes the quadratic phase factor exp[(ik/2f)(x²+y²)] that would otherwise
   appear in Fresnel diffraction. The field at the back focal plane is then
   the EXACT Fourier transform of the input — not an approximation. This is
   because the lens imparts a phase factor exp[−ik(ξ²+η²)/2f] that exactly
   cancels the Fresnel propagation kernel when input and output planes are
   at distances f from the lens.

3. **From FT to transfer functions**: In coherent imaging, the imaging system is
   linear in COMPLEX AMPLITUDE. The amplitude transfer function (CTF) is the
   pupil function P(ξ,η) evaluated at spatial frequencies: H(f_x,f_y) =
   P(λz f_x, λz f_y). The cutoff at f_c = NA/λ follows because the pupil
   truncates spatial frequencies with |f_⊥| > NA/λ. For incoherent imaging,
   the system is linear in INTENSITY → OTF = autocorrelation of CTF → doubled
   cutoff 2NA/λ.

4. **Connection to sampling theorem** (Nyquist — Shannon):
   The pupil's band-limited nature (CTF = 0 for f > f_c) means the image
   field is BAND-LIMITED to f_c = NA/λ. By Whittaker-Shannon, the minimum
   sampling interval for digital reconstruction is Δx = 1/(2f_c) = λ/(2NA).
   Undersampling below Nyquist → aliasing. In practice, pixel pitch ≤ λ/(4NA)
   (Nyquist-oversampling by 2×) is standard to capture the full OTF extent.

## Algorithm

```
1. COHERENT IMAGING (amplitude linear):
   U_i(x,y) = h(x,y) ∗ U_g(x,y)
   H(f_x,f_y) = P(λz f_x, λz f_y)  where P is the pupil function.
   Coherent cutoff: f_c = NA/λ. Rayleigh resolution: δx = 0.61λ/NA.

2. INCOHERENT IMAGING (intensity linear):
   I_i = |h|² ∗ I_g. OTF = H ★ H / ∫|H|²  (autocorrelation of CTF).
   Incoherent cutoff: 2NA/λ. Sparrow resolution: δx = 0.47λ/NA.

3. Fresnel diffraction (near field):
   U(x,y) = (e^{ikz}/iλz) ∫ U₀(ξ,η) exp[(ik/2z)((x−ξ)²+(y−η)²)] dξdη.
   Fresnel number: N_F = a²/λz. N_F ≫ 1 → geometric optics.
   N_F ∼ 1 → Fresnel. N_F ≪ 1 → Fraunhofer (far field = FT).

4. Fraunhofer diffraction (far field or lens focal plane):
   U(x,y) ∝ FT{U_aperture(ξ,η)} evaluated at f_x=x/λz, f_y=y/λz.

5. TALBOT SELF-IMAGING (Goodman §7.5, Rayleigh 1881):
   A periodic object (grating period Λ) illuminated by a plane wave
   produces EXACT self-images at multiples of the Talbot distance
   z_T = 2Λ²/λ. At z_T/2, a shifted self-image appears (phase-reversed
   for amplitude gratings). This is a near-field coherent effect: the
   Fresnel diffraction integral reproduces the object when the propagation
   phase exp(iπλz/Λ²) = 1. Applications: array illuminators, Lau
   interferometry, and as a test of spatial coherence.
   Breaks down at distances where Fresnel number per period ≫ 1 (goes
   to far-field Fraunhofer — use FT optics instead).

6. AMBIGUITY FUNCTION AND PULSE-SHAPE DESIGN (Papoulis §7, Goodman §6):
   The Woodward ambiguity function χ(τ,ν) = ∫ p(t) p*(t−τ) e^{i2πνt} dt
   connects pulse design to spatial filtering. In Fourier optics, the
   equivalent is the 2D ambiguity function over spatial frequency and
   defocus: A(f_x, Δz) describes how the OTF degrades with defocus.
   This links to ultrashort pulse design: the time-frequency ambiguity
   function for pulse shaping is the TEMPORAL ANALOG of the spatial
   ambiguity function for imaging. Use this connection to transfer
   pulse-shape design principles (apodization, phase-only filtering)
   from Fourier optics to temporal pulse shaping.
```

## Imaging Techniques (Goodman §7-9)

- **Phase contrast** (Zernike): π/2 phase shift of DC component →
  phase variations become intensity variations. Nobel 1953.
- **Schlieren**: spatial filter blocks half the FT → visualizes index gradients.
- **Dark field**: block DC → only scattered light imaged.
- **Apodization**: modify pupil function to suppress sidelobes (trade: wider main lobe).
- **Holography**: record |U_obj + U_ref|² → reconstruct U_obj by illuminating
  with U_ref. Off-axis (Leith-Upatnieks) separates twin images.

## Edge Cases

- **Coherence effects**: partially coherent illumination → effective OTF =
  OTF_coherent × γ(Δx) (coherence function). Speckle in coherent imaging.
  When spatial coherence is poor, switch to INCOHERENT imaging model —
  use OTF, not CTF.
- **Aberrations**: pupil function P includes phase error W(x,y) →
  H = P exp(ik W). Strehl ratio ≈ exp(−(2πσ_W/λ)²). Aberrations above
  λ/4 RMS break the diffraction limit — use adaptive optics (deformable
  mirror in pupil plane, wavefront sensor in image plane) or
  computational phase retrieval (Gerchberg-Saxton iterative FT).
- **High-NA (NA > 0.6)**: scalar theory (single field component) breaks down —
  use VECTOR DIFFRACTION (Richards-Wolf integral, Born & Wolf §8.8):
  E(r) = −(ikf/2π) ∫∫ a(k_x,k_y) e^{ik·r} dΩ/k_z, where a includes
  polarization rotation from the lens' high-NA ray bending. The focal
  spot becomes elliptical (smaller along polarization direction;
  longitudinal E_z component appears). Reference: Richards & Wolf,
  Proc. Roy. Soc. A 253, 358 (1959).
- **Nyquist violation**: pixel pitch > λ/(4NA) → aliasing in sampled images.
  Use anti-aliasing filter (physical or digital low-pass at f_c = NA/λ)
  or increase detector sampling density.

## Cross-References

- Goodman §3-9
- electrodynamics: reasoning.em.scattering_cross_section (Fraunhofer = far-field;
  parent edge: actively consumed in Derivation Sketch step 1)
- electrodynamics: reasoning.em.scalar_diffraction_kirchhoff (Fraunhofer IS the
  Fourier transform of the aperture — bidirectional: diffraction theory provides
  the Fraunhofer condition a²/λz≪1 that justifies the FT in Fourier optics)
