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
sign_convention: >
  Obliquity factor (cos θ₁ + cos θ₂)/2 in Kirchhoff derivation; RS-I uses
  cos θ (Dirichlet), RS-II uses cos θ_obs (Neumann). All three agree
  paraxially; discrepancies are O(λ/aperture).
---

# reasoning.em.scalar_diffraction_kirchhoff — Aperture → Diffraction Pattern

## Core Picture

When light passes through an aperture in an opaque screen, Huygens' principle
together with Kirchhoff's mathematical formulation gives the diffraction
pattern as an integral over the aperture (Born & Wolf §8, Goodman §3-4).

## Derivation Sketch (from Green's theorem → Kirchhoff integral)

Starting from `electrodynamics: reasoning.em.scattering_cross_section` (far-field
scattering as Fourier transform) and `landau-graph: reasoning.retarded_green_function`
(Green's function for Helmholtz):

**Helmholtz-Kirchhoff Integral Theorem** (Born & Wolf §8.3):

For scalar field U satisfying (∇² + k²)U = 0 in volume V, and Green's function
G = e^{ikr}/(4πr) satisfying (∇² + k²)G = −δ(r−r') (project default per
`physics-conventions: convention.green_functions`), Green's second identity:
```
  ∮_S [G ∂U/∂n − U ∂G/∂n] dS = ∫_V [G ∇²U − U ∇²G] dV = U(P)   for P∈V
                                                 = 0          for P∉V
```
Note: Jackson/Gaussian uses (∇²+k²)G=−4πδ→G=e^{ikr}/r and U=(1/4π)∮[·]dS.
Both give the same final integrand; the 1/(4π) lives inside G in our convention
vs. outside the integral in Jackson's. The diffraction integral below is
IDENTICAL in both conventions.

Hence the Helmholtz-Kirchhoff integral (project convention):
```
  U(P) = ∮_S [G ∂U/∂n − U ∂G/∂n] dS                     [eq.HK]
```
with the 1/(4π) absorbed in G itself.

**Kirchhoff's approximation** (the lossy step — mathematically inconsistent
but experimentally correct in the far field):

On the aperture Σ:  U = U_incident, ∂U/∂n = ∂U_inc/∂n
  (assume "screen invisible" — incident field unchanged inside aperture).
On the rest of the screen S−Σ: U = 0, ∂U/∂n = 0
  (assume "screen perfectly black" — zero field in geometric shadow).

Plug into [HK] with G = e^{ikr}/(4πr), ∂G/∂n ≈ ikG·cosθ for r≫λ:
```
  U(P) = −(ik/4π) ∫_Σ U₀(ξ,η) (e^{ikr}/r) (cos θ₁ + cos θ₂) dξ dη
```
(The 1/4π from G combines with the ik factor to produce the familiar prefactor.)
where θ₁ = angle between incident direction and aperture normal,
      θ₂ = angle between diffracted direction and aperture normal.

**WARNING** — Kirchhoff overspecifies the BCs (both U and ∂U/∂n on the closed
surface; the uniqueness theorem from `electrodynamics: reasoning.em.uniqueness_theorem_boundary_value`
says this is generally unsolvable). Rayleigh-Sommerfeld fixes this by using
only Dirichlet (G_D = 0 on screen) OR Neumann (∂G_N/∂n = 0) Green's functions:
- **RS-I (Dirichlet)**: obliquity = cos θ_observation
- **RS-II (Neumann)**: obliquity = cos θ_incidence
- **Kirchhoff**: obliquity = (cos θ_inc + cos θ_obs)/2  ← arithmetic mean
All three agree in the paraxial limit; differences are O(λ/distance).

## Algorithm

```
1. KIRCHHOFF DIFFRACTION INTEGRAL:
   U(P) = −(ik/4π) ∬_aperture U₀(ξ,η) (e^{ikr}/r)(cos θ₁+cos θ₂) dξdη
   For normal incidence: obliquity factor = (1+cos θ) ≈ 2.

2. Fresnel number: N_F = a²/λz  (a=aperture size, z=distance).
   N_F ≫ 1 → GEOMETRIC OPTICS (ray tracing valid).
   N_F ∼ 1 → FRESNEL DIFFRACTION (quadratic phase → Cornu spiral).
   N_F ≪ 1 → FRAUNHOFER DIFFRACTION (far field = Fourier transform).

3. FRESNEL (near field, spherical wavefront curvature matters):
   Approximate r = z + [(x−ξ)²+(y−η)²]/(2z) in exponent (keep quadratic):
   U(x,y) ∝ ∬ U₀ exp[(ik/2z)((x−ξ)²+(y−η)²)] dξdη.

   FRESNEL ZONE CONSTRUCTION (geometrical picture for Cornu spiral):
   Divide the aperture into HALF-PERIOD ZONES: each zone contributes
   λ/2 additional path-length difference from the edge. Adjacent zones
   have opposite phase → alternating contributions.
   Summing zone contributions as phasors → CORNU SPIRAL (parametric
   in Fresnel integrals C(w), S(w)):
     C(w) = ∫₀ʷ cos(πt²/2) dt,  S(w) = ∫₀ʷ sin(πt²/2) dt
   w = ξ √(2/λz) is the normalized coordinate. Tip-to-tail vector
   between w₁ and w₂ = relative amplitude.

   Fresnel zone plate: alternate transparent/opaque zones → focusing.
   N-th zone radius: r_N = √(Nλ f), focal length f = r_N²/(Nλ).

4. FRAUNHOFER (far field or lens focal plane):
   Drop ξ²,η² terms in exponent (condition: a²/λz ≪ 1, i.e., N_F ≪ 1):
   exp[(ik/2z)(x²−2xξ+ξ² + ...)] → exp[(ik/2z)(x²+y²)] · exp[−ik(xξ+yη)/z]
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

- **Vector diffraction** (high NA >0.5): scalar Kirchhoff fails. Use Richards-Wolf
  integral (Born & Wolf §8.8): Debye-Wolf diffraction integral with polarization
  rotation, 3D focal field E(r) = −(ikf/2π) ∬ a(k_x,k_y) e^{ik·r} dΩ/k_z.
- **Near-field (sub-wavelength)**: evanescent components, requires full
  Maxwell, not scalar diffraction. Use angular spectrum method with
  k_z = √(k²−k_x²−k_y²) → imaginary for k_∥ > k → near-field evanescent.

## Cross-References

- Born & Wolf §8, Goodman §3-4, Jackson §10.5-10.10
- electrodynamics: reasoning.em.scattering_cross_section (Fraunhofer = far-field
  scattering; parent edge: scattering theory → diffraction as aperture scattering)
- electrodynamics: reasoning.em.uniqueness_theorem_boundary_value (Kirchhoff BC
  inconsistency explained by uniqueness theorem)
- optics: reasoning.optics.fourier_optics_transfer_function (Fraunhofer IS FT
  relation → lens-based FT implementation. Bidirectional: FT optics uses the
  Fraunhofer condition derived here)
