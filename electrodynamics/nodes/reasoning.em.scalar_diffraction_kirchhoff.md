---
skill_id: reasoning.em.scalar_diffraction_kirchhoff
type: reasoning
summary_50t: >
  Scalar diffraction integral: U(P)=−(ik/4π)∫U₀(e^{ikr}/r)(cos θ₁+cos θ₂)dS.
  Fresnel number N_F=a²/λz classifies regimes. N_F≫1→geometric, N_F∼1→Fresnel
  (Cornu spiral), N_F≪1→Fraunhofer (FT of aperture). Babinet: complementary
  apertures give same diffraction pattern (outside direct beam).
trigger:
  - computing diffraction pattern from aperture of known shape
  - identifying diffraction regime by Fresnel number
reasoning_role: scalar_diffraction
parent: reasoning.em.scattering_cross_section
retrieval_cost: 1
---

# reasoning.em.scalar_diffraction_kirchhoff — Aperture → Diffraction Pattern

## Core Picture

When light passes through an aperture in an opaque screen, Huygens' principle
together with Kirchhoff's mathematical formulation gives the diffraction
pattern as an integral over the aperture (Born & Wolf §8, Goodman §3-4).

## Algorithm

```
1. KIRCHHOFF DIFFRACTION INTEGRAL:
   U(P) = −(ik/4π) ∬_aperture U₀(ξ,η) (e^{ikr}/r)(cos θ₁+cos θ₂) dξdη
   where θ₁=angle between incident direction and aperture normal,
   θ₂=angle between diffracted direction and aperture normal.
   For normal incidence: obliquity factor = (1+cos θ) ≈ 2.

2. Fresnel number: N_F = a²/λz  (a=aperture size, z=distance).
   N_F ≫ 1 → GEOMETRIC OPTICS (ray tracing valid).
   N_F ∼ 1 → FRESNEL DIFFRACTION (quadratic phase → Cornu spiral).
   N_F ≪ 1 → FRAUNHOFER DIFFRACTION (far field = Fourier transform).

3. FRESNEL (near field, spherical wavefront curvature matters):
   U(x,y) ∝ ∬ U₀ exp[(ik/2z)((x−ξ)²+(y−η)²)] dξdη.
   Straight edge → Cornu spiral → Fresnel integrals C(w), S(w).
   Fresnel zone plate: alternate transparent/opaque zones → focusing.

4. FRAUNHOFER (far field or lens focal plane):
   U(x,y) ∝ ∬ U₀ exp[−ik(xξ+yη)/z] dξdη = FT{U₀} at f_x=x/λz.
   Rectangular slit a×b → I ∝ sinc²(πa sin θ_x/λ)·sinc²(πb sin θ_y/λ).
   Circular aperture D → I ∝ [2J₁(kD sin θ/2)/(kD sin θ/2)]². Airy disk.

5. BABINET PRINCIPLE: complementary screens give IDENTICAL diffraction
   patterns except in the direct beam (geometric shadow region).
```

## Key Patterns

**Single slit** (width a): I ∝ sinc²(πa sin θ/λ). Minima at a sin θ=mλ (m≠0).
**Double slit** (separation d): I ∝ cos²(πd sin θ/λ) × [sinc²(πa sin θ/λ)].
**Grating** (N slits): I ∝ [sin(Nπd sin θ/λ)/sin(πd sin θ/λ)]².
Blaze angle: shift single-slit envelope to desired diffraction order.

## Edge Cases

- **Vector diffraction** (high NA >0.5): scalar Kirchhoff fails, use
  Richards-Wolf (Born & Wolf §8.8) — polarization matters.
- **Near-field (sub-wavelength)**: evanescent components, requires full
  Maxwell, not scalar diffraction.

## Cross-References

- Born & Wolf §8, Goodman §3-4, Jackson §10.5-10.10
- electrodynamics: reasoning.em.scattering_cross_section (Fraunhofer = far-field scattering)
- optics: reasoning.optics.fourier_optics_transfer_function (lens-based FT implementation)
