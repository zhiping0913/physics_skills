---
skill_id: knowledge.em.scattering_mie
type: knowledge
summary_50t: >
  Mie solution for sphere: a_l,b_l from matching at r=a. Rayleigh limit (ka≪1):
  σ∝ω⁴. Optical theorem: σ_ext=(4π/k)Im[f(0)]. Born approximation for weak
  scatterers. Kirchhoff diffraction: Fresnel (near) and Fraunhofer (far) zones.
trigger:
  - computing scattering from spherical particles, diffraction patterns
reasoning_role: scattering_knowledge
parent: reasoning.em.scattering_cross_section
retrieval_cost: 1
---

# knowledge.em.scattering_mie

**Mie coefficients** for sphere radius a, relative index m=n_sph/n_med, x=ka:
a_l = [mψ_l(mx)ψ'_l(x)−ψ_l(x)ψ'_l(mx)] / [mψ_l(mx)ξ'_l(x)−ξ_l(x)ψ'_l(mx)]
b_l = [ψ_l(mx)ψ'_l(x)−mψ_l(x)ψ'_l(mx)] / [ψ_l(mx)ξ'_l(x)−mξ_l(x)ψ'_l(mx)]
where ψ_l(z)=z j_l(z), ξ_l(z)=z h_l^(1)(z).

**Rayleigh limit** (x≪1): σ_scat = (8π/3)k⁴a⁶|(m²−1)/(m²+2)|²
Angular: unpolarized → (1+cos²θ). Polarized 90° scattering.

**Geometric optics** (x≫1): σ_scat → 2πa² (extinction paradox: twice geometric).
Plus strong forward diffraction peak (Airy pattern for large spheres).

**Born approximation** (|m−1|≪1 and (m−1)ka≪1):
f(k,k') ∝ ∫ ε(r')e^{i(k−k')·r'} dV' — scattering amplitude = FT of permittivity.
Valid for soft scatterers (biological tissue, atmosphere).

**Kirchhoff diffraction**: For aperture in screen —
Fraunhofer (far field, kD²/R≪1): E(θ)∝FT[aperture shape]
Rectangular slit a×b: I∝sinc²(ka sin θ_x/2)·sinc²(kb sin θ_y/2). First minimum at θ=λ/a.
Circular aperture D: I∝[2J₁(kD sin θ/2)/(kD sin θ/2)]². Airy disk: θ_min=1.22λ/D.

**Optical theorem**: σ_ext = (4π/k)Im[f(0)]. Independent of target shape.

- Jackson §10, Born & Wolf §8.3, §13.5
