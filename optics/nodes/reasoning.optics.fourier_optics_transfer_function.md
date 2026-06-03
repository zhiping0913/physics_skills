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
references:
  - electrodynamics: reasoning.em.scattering_cross_section (Fraunhofer diffraction)
---

# reasoning.optics.fourier_optics_transfer_function — Lens → FT → Image

## Core Picture

A lens performs a FOURIER TRANSFORM (Goodman §4-6). The field at the back
focal plane of a lens is the Fourier transform of the field at the front
focal plane. This transforms the problem of image formation from convolution
in real space to MULTIPLICATION in frequency space.

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
- **Aberrations**: pupil function P includes phase error W(x,y) →
  H = P exp(ik W). Strehl ratio ≈ exp(−(2πσ_W/λ)²).

## Cross-References

- Goodman §3-9
- electrodynamics: reasoning.em.scattering_cross_section (Fraunhofer = far-field)
- electrodynamics: reasoning.em.scalar_diffraction_kirchhoff (Fraunhofer IS the
  Fourier transform of the aperture — bidirectional: diffraction theory provides
  the Fraunhofer condition a²/λz≪1 that justifies the FT in Fourier optics)
