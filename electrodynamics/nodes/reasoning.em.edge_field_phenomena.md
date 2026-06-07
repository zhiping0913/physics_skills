---
skill_id: reasoning.em.edge_field_phenomena
type: reasoning
summary_50t: >
  Edge fields connect Meixner near-edge singularities to Keller GTD far-edge
  diffraction. Near a wedge of angle α, φ ~ ρ^ν sin(νψ), ν = π/α, so
  E ~ ρ^{ν-1}; for a half-plane α=2π, E ~ ρ^{-1/2}. Far away, an edge launches
  a cylindrical diffracted ray ψ_d ~ D e^{ikr}/√r.
trigger:
  - fields near a sharp conducting or dielectric edge
  - diffraction by a half-plane, wedge, crack, or corner
  - matching local singular fields to far-field asymptotics
reasoning_role: edge_singularity_to_diffraction
parent: mathematics.steepest_descent
retrieval_cost: 1
sign_convention: time-harmonic e^{-iωt}; outgoing factor e^{ikr}
---

# reasoning.em.edge_field_phenomena — Edge Singularity → Diffracted Ray

## Core Picture

A sharp edge is not just a small geometric defect. It creates a local singular
field and also launches a far-zone diffracted wave. The near description is the
Meixner edge condition; the far description is Keller's geometrical theory of
diffraction (GTD). They are two asymptotic faces of the same quasi-cylindrical
edge wave.

```
near edge:  local wedge eigenfunction     E ~ ρ^{ν-1}
far field:  cylindrical diffracted ray    ψ_d ~ D(θ_s,θ_0) e^{ikr}/√r
```

The singularity is integrable: the field may diverge while the energy in a small
neighborhood remains finite.

## Near Field: Meixner Wedge Singularity

Use polar coordinates (ρ,ψ) around the edge cross-section. For a local wedge of
interior angle α, the quasistatic leading term satisfies Laplace's equation:

```
∇²φ = 0,       0 < ψ < α.
```

With homogeneous boundary conditions on the wedge faces, separation of variables
gives

```
φ(ρ,ψ) ~ ρ^ν sin(νψ),      ν = π/α        fundamental mode
```

(up to cosine vs sine depending on whether the boundary condition is Dirichlet,
Neumann, PEC polarization, etc.). Since E = -∇φ,

```
E ~ ρ^{ν-1}.
```

For a perfectly conducting half-plane, the exterior wedge angle is α = 2π, so

```
ν = 1/2,       E ~ ρ^{-1/2}.
```

This is the canonical square-root edge singularity. It is allowed by Meixner's
condition because the local energy integral is finite:

```
∫_0^ε |E|² ρ dρ  ~  ∫_0^ε ρ^{2ν-1} dρ  < ∞     for ν > 0.
```

For full EM wedges, the precise exponents depend on polarization, dielectric
contrast, and PEC vs penetrable boundary conditions, but the logic is the same:
solve the local wedge eigenvalue problem and select the finite-energy exponents.

## Far Field: Keller GTD Edge Diffraction

Geometrical optics (GO) predicts incident, reflected, and transmitted rays, but
it is discontinuous at shadow boundaries. Keller's GTD adds diffracted rays that
emanate from edges according to a generalized Fermat principle.

For a 2D edge/half-plane, the leading outgoing diffracted field has cylindrical
spreading:

```
ψ_d(r,θ_s) ~ D(θ_s, θ_0) e^{ikr} / √r,
```

where θ_0 is the incident angle, θ_s is the observation/scattering angle, and
D(θ_s,θ_0) is the diffraction coefficient determined by the local wedge problem.
For a 3D edge, the same idea applies along the cone of diffracted rays, with the
spreading factor modified by the ray geometry.

GTD is an asymptotic high-frequency theory: k times the source-edge-observer
length scale must be large. Close to shadow boundaries the original Keller
coefficient is singular; uniform theory of diffraction (UTD) replaces it with a
Fresnel-transition function.

## Why Near and Far Are the Same Edge Wave

The wedge eigenfunction is local in ρ, while the GTD ray is the large-r limit of
an edge-launched cylindrical wave. A useful matching picture is:

```
1. The incident field drives surface currents/charges that are singular at the edge.
2. The Meixner exponent fixes the allowed local behavior and edge-source strength.
3. The edge source radiates a cylindrical wave along the exterior domain.
4. Steepest-descent evaluation of its spectral/Sommerfeld representation gives
   the far-zone GTD form e^{ikr}/√r and the diffraction coefficient D.
```

Thus the square-root singularity near a half-plane and the 1/√r diffracted ray
far from that half-plane are connected by one quasi-cylindrical edge field, not
by two unrelated mechanisms.

## Algorithm: From Edge Geometry to Asymptotic Field

```
1. Identify the local edge cross-section and wedge angle α.
2. Solve the local eigenvalue problem in wedge coordinates:
       φ ~ ρ^ν [A sin(νψ) + B cos(νψ)]
   with the correct EM/acoustic/elastic/quantum boundary conditions.
3. Select Meixner-admissible exponents: finite local energy or finite flux.
4. Use the leading exponent to characterize charge/current/stress enhancement
   near the edge.
5. For high-frequency far fields, construct GO rays plus Keller diffracted rays.
6. Use the wedge diffraction coefficient D(θ_s,θ_0) and cylindrical spreading:
       ψ_d ~ D(θ_s,θ_0) e^{ikr}/√r.
7. Near shadow boundaries, replace GTD by UTD/uniform asymptotics to remove
   artificial divergences.
```

## Cross-Domain Table

| Domain | Local singular field | Far/asymptotic manifestation |
|---|---|---|
| EM PEC wedge/half-plane | Surface charge/current and E,H scale as wedge powers; half-plane gives E ~ ρ^{-1/2} for the singular polarization | Keller/GTD edge-diffracted rays restore fields in shadow regions; UTD smooths shadow boundaries |
| EM dielectric wedge | Exponents depend on permittivity contrast and TE/TM coupling; singularity may be weaker or stronger than PEC | Diffracted and transmitted edge waves with material-dependent D(θ_s,θ_0) |
| Acoustic wedge | Pressure or velocity potential satisfies scalar Helmholtz/Laplace wedge problem with Dirichlet/Neumann faces | Sound diffraction around barriers; cylindrical edge wave ∝ e^{ikr}/√r in 2D |
| Crack tips in elasticity | Stress intensity fields scale as σ ~ r^{-1/2}; finite energy release rate selects the square-root singularity | Far elastic wave scattering and crack-tip radiation encode the same tip singularity |
| Quantum corners | Schrödinger/Laplace eigenfunctions in polygonal domains have corner powers r^ν | Corner diffraction and spectral shifts; semiclassical rays acquire diffractive corner contributions |

## Edge Cases / Checks

- Rounded edge: singularity is cut off at the radius of curvature; use wedge
  asymptotics only for radius_of_curvature ≪ ρ ≪ wavelength/geometric scale.
- Finite conductivity: PEC square-root behavior is smoothed within skin-depth and
  material boundary layers.
- Exact exponent: α alone gives the scalar Dirichlet/Neumann prototype. Full EM
  dielectric wedges require the coupled vector wedge characteristic equation.
- GTD validity: needs kr ≫ 1 and fails at caustics or shadow boundaries unless
  replaced by a uniform approximation.

## Cross-References

- mathematics-theorems: mathematics.steepest_descent (far-field extraction from
  spectral edge integrals)
- electrodynamics: reasoning.em.scalar_diffraction_kirchhoff (aperture/edge
  diffraction as wave asymptotics)
- electrodynamics: reasoning.em.scattering_cross_section (far-field amplitudes
  and cross sections)
- Meixner, J., "The behavior of electromagnetic fields at edges," IEEE TAP 20,
  442-446 (1972)
- Keller, J.B., "Geometrical theory of diffraction," JOSA 52, 116-130 (1962)
