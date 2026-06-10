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
parent: landau-graph:reasoning.small_parameter_expansion
sign_convention: time-harmonic e^{−iωt}; outgoing scattered wave e^{ikr}/r
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

## Derivation Sketch

Starting from `landau-graph: reasoning.small_parameter_expansion` we have the
pattern: identify a small dimensionless parameter → expand the governing
equation → truncate at leading order. For scattering, the size parameter
ka = 2πa/λ controls three distinct regimes:

**Key non-obvious step — the optical theorem and the extinction paradox**:
The extinction cross section σ_ext = σ_scat + σ_abs is given by the FORWARD
scattering amplitude alone: σ_ext = (4π/k)Im[f(0)]. This is a consequence of
energy conservation (unitarity of the S-matrix): the forward-scattered wave
INTERFERES with the incident wave, removing power from the forward direction
to feed scattered power into all other directions. For a large opaque object
(ka ≫ 1), σ_ext → 2πa² — TWICE the geometric cross section πa². The "extra"
πa² comes from diffraction: the shadow region creates an equal amount of
scattered power beyond direct interception (the **extinction paradox**).

**Born approximation** (weak scatterer, |ε−1| ≪ 1): Replace the total field
inside the scatterer by the incident field → f(k,k') ∝ ∫[ε(r')−1]e^{i(k−k')·r'}dV'.
This is the 3D Fourier transform of the dielectric contrast. Valid when
|ε−1|ka ≪ 1 (single scattering). When this breaks down (strong scatterer),
switch to Mie theory (exact for sphere) or T-matrix method (arbitrary shape).

**Polarization scattering matrix (Stokes-Mueller formalism)**:
The scattered field relates to incident field via the 2×2 Jones matrix J:
(E_s∥, E_s⟂)^T = (e^{ikr}/r) J·(E_i∥, E_i⟂)^T. For partially polarized
light, use the 4×4 Mueller matrix M relating Stokes vectors:
S_s = (1/r²) M·S_i. The 16 Mueller elements encode all polarization
properties: depolarization, diattenuation, retardance. For spherical
particles, symmetry reduces M to 4 independent parameters (Bohren & Huffman §3).

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
This is a consequence of ENERGY CONSERVATION (unitarity of S-matrix). It holds
for ANY target, not just spheres.

### Asymptotic methods for electrically large scatterers
(EM Radiation, Scattering, and Diffraction 2021, Ch.16)

When the scatterer size D ≫ λ, full-wave methods become prohibitively
expensive. Asymptotic techniques exploit the short-wavelength limit:

- **GTD (Geometrical Theory of Diffraction)** — Keller (1962): extends
  GO with diffracted rays from edges, tips, and creeping waves on
  smooth convex surfaces. Diffraction coefficient D(φ,φ') from
  canonical wedge problem.
- **UTD (Uniform Theory of Diffraction)** — Kouyoumjian & Pathak (1974):
  removes GTD's singularities at shadow/reflection boundaries using
  Fresnel integral transition functions. Uniformly valid across all
  observation angles.
- **PO (Physical Optics)** — surface current approximation J_s ≈ 2n̂×H_i
  on lit surfaces, J_s=0 in shadow. Accurate near specular directions;
  fails at wide angles and for edge diffraction.

These methods connect to `em.dyadic_green_function` (full-wave kernel)
and `em.scalar_diffraction_kirchhoff` (the scalar precursor to PO).

## Edge Cases

- **Rayleigh-Gans-Debye (RGD) regime**: |ε−1| ≪ 1 but ka NOT ≪ 1 — use Born
  approximation for arbitrary size. When |ε−1|ka > 1, RGD breaks down — switch
  to Mie theory for spheres or anomalous diffraction (AD) approximation
  for ka ≫ 1 with moderate |ε−1|.
- **Resonant scattering** (Mie resonances): At specific ka, a_l or b_l ≈ 1 →
  sharp peaks in σ_scat. These are morphology-dependent resonances (MDRs) or
  "whispering gallery" modes — analyze with complex angular momentum (CAM)
  theory for physical interpretation, not just numerical Mie code.
- **Multiple scattering**: When scatterer density is high (mean free path
  ℓ ≪ sample size), single-scattering theory breaks down — switch to radiative
  transfer equation (RTE) or full Maxwell solver (DDA, FDTD, T-matrix
  superposition).

## Cross-References

- Jackson §10.1-10.11
- Born & Wolf §8.3 (Kirchhoff diffraction), §13.5 (Mie theory)
- landau-graph: reasoning.small_parameter_expansion (ka controls approximation)
- electrodynamics: reasoning.em.fresnel_interface_reflection_refraction
  (specular reflection = Fresnel limit; rough surface generalizes to scattering
  via perturbation theory — bidirectional)
