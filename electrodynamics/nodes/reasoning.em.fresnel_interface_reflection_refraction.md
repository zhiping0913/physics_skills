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
---

# reasoning.em.fresnel_interface_reflection_refraction — Boundary → r, t

## Core Picture

When a plane EM wave strikes a planar interface between two media, the boundary
conditions on E and H determine the reflected and transmitted amplitudes via
the FRESNEL COEFFICIENTS (Jackson §7.3, Griffiths §9.3, Born & Wolf §1.5).
This is the fundamental building block of ALL interface optics.

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

   p-pol (TM):
   r_p = (n₂ cos θ_i − n₁ cos θ_t) / (n₂ cos θ_i + n₁ cos θ_t)
   t_p = 2 n₁ cos θ_i / (n₂ cos θ_i + n₁ cos θ_t)

4. Power reflectance: R_s = |r_s|², R_p = |r_p|².
   Power transmittance: T_s = (n₂ cos θ_t/n₁ cos θ_i)|t_s|² (same for p).

5. Brewster angle: r_p = 0 → tan θ_B = n₂/n₁. Only for p-pol.
   At θ_B, reflected light is purely s-polarized.

6. Total internal reflection (TIR): n₁ > n₂, θ_i > θ_c = arcsin(n₂/n₁).
   cos θ_t = i√((n₁/n₂)² sin²θ_i − 1) → |r|=1, evanescent transmitted field.
   Goos-Hänchen shift: lateral displacement of reflected beam Δ ∼ λ.
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
- **Thin films**: multiple reflections → interference, Fabry-Perot etalon.
- **Inhomogeneous waves**: non-plane-wave incident beams (Gaussian) have
  modified reflection (Goos-Hänchen, Imbert-Fedorov shifts).

## Cross-References

- Jackson §7.3-7.4, Griffiths §9.3, Born & Wolf §1.5
- electrodynamics: reasoning.em.waveguide_mode_decomposition (walls = Fresnel)
- optics: reasoning.optics.fourier_optics_transfer_function (coating MTF)
