---
skill_id: reasoning.em.scattering_cross_section
type: reasoning
summary_50t: >
  dσ/dΩ = (scattered power/solid angle)/incident flux. Three regimes:
  ka≪1: Rayleigh ∝ ω⁴; ka∼1: Mie (exact spherical harmonics);
  ka≫1: geometric optics. Optical theorem: σ_tot=(4π/k)Im[f(0)].
trigger:
  - EM wave incident on finite target
  - need angular distribution of scattered radiation
  - computing extinction, absorption, scattering efficiencies
reasoning_role: scattering_theory
parent: reasoning.small_parameter_expansion
retrieval_cost: 1
references:
  - landau-graph: reasoning.small_parameter_expansion
---

# reasoning.em.scattering_cross_section — Incident Wave → Angular Distribution

## Core Picture

An incident plane wave E_i = E₀ e^{i(kz−ωt)} hits a target. The scattered
field in the far zone is an OUTGOING spherical wave:

```
E_s(r) → f(k,k') E₀ e^{ikr}/r   as r → ∞
```

where f(k,k') is the SCATTERING AMPLITUDE (depends on incident direction k
and scattered direction k'). All observable quantities follow from f.

## Algorithm (Jackson §10)

```
1. Define differential cross section:
   dσ/dΩ = |f(k,k')|² = (r²⟨S_s⟩·n)/(|⟨S_i⟩|)

2. Total cross sections:
   σ_scat = ∫ (dσ/dΩ) dΩ  (integrated scattered power / incident flux)
   σ_ext = σ_scat + σ_abs  (EXTINCTION = scattering + absorption)
   Optical theorem: σ_ext = (4π/k) Im[f(k,k)] — forward amplitude
   determines total extinction (not just scattering).

3. Three regimes by size parameter ka = 2πa/λ:
```

## Regime I: Rayleigh Scattering (ka ≪ 1)

Target ≪ wavelength → induced dipole moment → radiation from oscillating dipole.

```
σ_scat = (8π/3)(k⁴a⁶)|(ε−ε₀)/(ε+2ε₀)|²  ∝ ω⁴ (blue sky, red sunset)
Angular pattern: ∝ sin²θ (dipole radiation)
Polarization: scattered light polarized perpendicular to scattering plane at 90°
```

## Regime II: Mie Scattering (ka ∼ 1)

Exact solution for SPHERE using spherical wave expansion (Born & Wolf §13.5):

```
1. Expand incident plane wave in spherical harmonics:
   e^{ikz} = Σ i^l(2l+1)j_l(kr)P_l(cos θ)

2. Expand scattered wave with outgoing Hankel functions: h_l^(1)(kr)

3. Match boundary conditions at r=a → Mie coefficients a_l, b_l:
   a_l = [mψ_l(mx)ψ'_l(x)−ψ_l(x)ψ'_l(mx)]/[mψ_l(mx)ξ'_l(x)−ξ_l(x)ψ'_l(mx)]
   where m = n_sphere/n_medium, x = ka.

4. Cross sections:
   σ_scat = (2π/k²) Σ (2l+1)(|a_l|²+|b_l|²)
   σ_ext = (2π/k²) Σ (2l+1) Re(a_l+b_l)
```

## Regime III: Geometric Optics (ka ≫ 1)

Wave optics → ray optics limit. σ_scat → 2πa² (twice geometric cross section —
the "extinction paradox"). Diffraction contributes equally to direct interception.

## Optical Theorem

σ_ext = (4π/k) Im[f(0)] — a purely FORWARD quantity determines TOTAL extinction.
This is a consequence of ENERGY CONSERVATION (unitarily of S-matrix). It holds
for ANY target, not just spheres.

## Cross-References

- Jackson §10.1-10.11
- Born & Wolf §8.3 (Kirchhoff diffraction), §13.5 (Mie theory)
- landau-graph: reasoning.small_parameter_expansion (ka controls approximation)
