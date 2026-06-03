---
skill_id: reasoning.em.fresnel_interface_reflection_refraction
type: reasoning
summary_50t: >
  Plane wave at planar interface: E∥, E⟂ boundary conditions → Fresnel
  coefficients r_s=(n₁cosθ_i−n₂cosθ_t)/(...), Brewster θ_B=arctan(n₂/n₁),
  TIR for θ>θ_c=arcsin(n₂/n₁). Complex ñ for metals. Power: R=|r|², T=1−R.
trigger:
  - EM wave incident on material interface at arbitrary angle
  - computing reflection/transmission, Brewster angle, total internal reflection
reasoning_role: fresnel_coefficients
parent: reasoning.em.waveguide_mode_decomposition
retrieval_cost: 1
sign_convention: >
  r_p follows the VERDET (B-tangential) convention (E_r tangential component
  has same sign at normal incidence). Born & Wolf uses the opposite sign
  (E-tangential flips at normal). Both are equivalent; check before comparing.
---

# reasoning.em.fresnel_interface_reflection_refraction — Boundary → r, t

## Core Picture

When a plane EM wave strikes a planar interface between two media, the boundary
conditions on E and H determine the reflected and transmitted amplitudes via
the FRESNEL COEFFICIENTS (Jackson §7.3, Griffiths §9.3, Born & Wolf §1.5).
This is the fundamental building block of ALL interface optics.

## Derivation Sketch (from waveguide mode decomposition → boundary value)

Starting from `electrodynamics: reasoning.em.waveguide_mode_decomposition`
(matching tangential fields at conducting walls), the dielectric interface
generalizes: instead of E_∥=0 on walls, we have CONTINUITY of tangential
components across z=0.

**Boundary conditions at z=0 interface** (no surface current/charge):
- **E_∥ continuous**: E_t,1(z=0) = E_t,2(z=0)
- **H_∥ continuous**: H_t,1(z=0) = H_t,2(z=0)

For plane waves e^{i(k·r−ωt)}, these become algebraic constraints that
determine reflected and transmitted amplitudes uniquely.

**s-polarization (TE, E along ŷ, perpendicular to plane of incidence)**:

E continuity (all tangential):
  (E_i + E_r) = E_t                                            [eq.A]

H_∥ continuity. Using H = (k×E)/(ωμ) and μ=μ₀ (non-magnetic):
  k_{iz}E_i − k_{iz}E_r = k_{tz}E_t                            [eq.B]
(Note: k_{rz} = −k_{iz} because reflected wave has k_z → −k_z.)

With k_z = n k₀ cos θ (k₀ = ω/c):
  [eq.A] ÷: r_s ≡ E_r/E_i = (n₁ cos θ_i − n₂ cos θ_t) / (n₁ cos θ_i + n₂ cos θ_t)
  [eq.B] ÷: t_s ≡ E_t/E_i = 2 n₁ cos θ_i / (n₁ cos θ_i + n₂ cos θ_t)

**p-polarization (TM, H along ŷ, E in plane)**:

H continuity (all tangential, single component ŷ):
  (H_i + H_r) = H_t                                            [eq.C]

E_∥ continuity. Using E = (k×H)/(−ωε), the x-component is E_x = (k_z H)/(ωε):
  (k_{iz}/n₁²)(H_i − H_r) = (k_{tz}/n₂²) H_t                    [eq.D]
(ε = n² ε₀ absorbs into the n² factor.)

Solve [eq.C] and [eq.D]:
  r_p ≡ H_r/H_i = (n₂ cos θ_i − n₁ cos θ_t) / (n₂ cos θ_i + n₁ cos θ_t)
  t_p ≡ H_t/H_i = 2 n₁ cos θ_i / (n₂ cos θ_i + n₁ cos θ_t)

**Sign convention**: r_p above is H-field ratio (Verdet convention).
In E-field ratio form, r_p(E) = −r_p(H). Born & Wolf uses r_p(E);
either convention is fine as long as it's stated. Power R = |r|² is unambiguous.

## Algorithm

```
1. Snell's law: n₁ sin θ_i = n₂ sin θ_t.

2. Define polarization relative to plane of incidence (k_i, n̂):
   s-polarization (TE, E ⟂ plane): E is tangent to interface on both sides.
   p-polarization (TM, H ⟂ plane): H is tangent, E has normal component.

3. FRESNEL COEFFICIENTS (SI, non-magnetic μ=μ₀):

   s-pol (TE):
   r_s = (n₁ cos θ_i − n₂ cos θ_t) / (n₁ cos θ_i + n₂ cos θ_t)
   t_s = 2 n₁ cos θ_i / (n₁ cos θ_i + n₂ cos θ_t)

   p-pol (TM, Verdet convention):
   r_p = (n₂ cos θ_i − n₁ cos θ_t) / (n₂ cos θ_i + n₁ cos θ_t)
   t_p = 2 n₁ cos θ_i / (n₂ cos θ_i + n₁ cos θ_t)

4. Power reflectance: R_s = |r_s|², R_p = |r_p|².
   Power transmittance: T_s = (n₂ cos θ_t/n₁ cos θ_i)|t_s|² (same for p).

5. Brewster angle: r_p = 0 → tan θ_B = n₂/n₁. Only for p-pol.
   At θ_B, reflected light is purely s-polarized.

6. Total internal reflection (TIR): n₁ > n₂, θ_i > θ_c = arcsin(n₂/n₁).
   cos θ_t = i √((n₁/n₂)² sin²θ_i − 1) → |r| = 1, evanescent transmitted field.
   Penetration depth into medium 2: d = 1/Im(k_z) = λ/(2π√(n₁²sin²θ_i − n₂²)).
   Goos-Hänchen shift: Δ_∥ = −(λ/2πn₁)(dφ_r/dθ_i) where φ_r = arg(r).
   For TIR, Δ_∥ ∼ λ (lateral shift of reflected beam). Born & Wolf §1.5.4.

7. TRANSFER MATRIX FOR THIN FILMS (Born & Wolf §1.6):
   Each layer j of thickness d_j: 2×2 matrix M_j connecting (E,H)_top → (E,H)_bot.
   M_j = [ cos δ_j          (i/η_j) sin δ_j      ]
         [ i η_j sin δ_j    cos δ_j               ]
   where δ_j = 2π n_j d_j cos θ_j / λ, η_j = n_j cos θ_j (TE) or n_j/cos θ_j (TM).
   Stack: M_total = M_1 M_2 ... M_N. r = (η₀(M₁₁+M₁₂η_s)−(M₂₁+M₂₂η_s)) / (denom).
```

## Key Special Cases

**Normal incidence** (θ_i=0): r = (n₁−n₂)/(n₁+n₂), R = |(n₁−n₂)/(n₁+n₂)|².
Glass (n=1.5): R ≈ 4% per surface.

**Metals** (ñ = n+iκ): r, t become complex → phase shift on reflection.
R = |r|², no transmission for thick metal. Skin depth δ = λ/(2πκ).

**Grazing incidence** (θ_i → 90°): R → 1 for both polarizations.
X-ray mirrors use this (θ < θ_c ∼ √(2δ), δ = 1−n ≪ 1).

## Edge Cases

- **Anisotropic media**: Fresnel generalized with walk-off, double refraction.
  Use D = ε:E, determine k from index ellipsoid (Born & Wolf §14). Walk-off
  angle between Ŝ (Poynting) and k̂ follows tan ρ = (1/n)(dn/dθ).
- **Thin films**: multiple reflections → interference, Fabry-Perot. Use
  transfer matrix algorithm (step 7 above).
- **Inhomogeneous waves**: non-plane-wave incident beams (Gaussian) have
  modified reflection: Goos-Hänchen and Imbert-Fedorov shifts. Fedorov-Imbert
  (spin) shift is typically λ/100 level — requires beam mode expansion.
- **Absorbing substrate (metals)**: ñ = n+iκ → Fresnel coefficients with
  complex Snell's law: n₁ sin θ_i = ñ₂ sin θ_t (sin θ_t complex, "inhomogeneous
  wave" in medium 2). Azzam & Bashara §4.

## Cross-References

- Jackson §7.3-7.4, Griffiths §9.3, Born & Wolf §1.5-1.6, Azzam & Bashara §4
- electrodynamics: reasoning.em.waveguide_mode_decomposition (waveguide walls =
  TIR boundary; Fresnel is the dielectric counterpart)
- electrodynamics: reasoning.em.scattering_cross_section (rough interface →
  reflection generalizes to scattering; specular = Fresnel limit)
- optics: reasoning.optics.fourier_optics_transfer_function (thin-film coatings
  → coating MTF; transfer matrix feeds optical design)
