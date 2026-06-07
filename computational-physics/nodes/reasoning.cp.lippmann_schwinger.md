---
skill_id: reasoning.cp.lippmann_schwinger
type: reasoning
summary_50t: >
  Lippmann-Schwinger rewrites scattering in a known background as
  ψ=ψ_inc+∫G V ψ dV. For EM volume integral equations,
  E=E_inc+ω²μ_b∫G̿_b·(ε-ε_b)E dV. Neumann iteration gives the Born series;
  volume MoM discretizes the integral equation into a dense contrast matrix.
trigger:
  - deriving volume integral equations for dielectric or inhomogeneous scatterers
  - using Born or Rytov approximations for weak scattering
  - mapping EM scattering methods to quantum, acoustic, or elastic Lippmann-Schwinger forms
reasoning_role: lippmann_schwinger_volume_ie
parent: reasoning.em.dyadic_green_function
retrieval_cost: 1
---

# reasoning.cp.lippmann_schwinger — background Green function + contrast source

## Core Picture

The Lippmann-Schwinger equation splits a scattering problem into:

1. a known background problem with outgoing Green function G, and
2. a contrast source Vψ induced by the unknown total field inside the scatterer.

The universal form is
```
ψ(r) = ψ_inc(r) + ∫_D G(r,r') V(r') ψ(r') dV'.
```
It is a volume integral equation (VIE): solve only where the material contrast
V is nonzero, then evaluate the field anywhere using the same Green function.

## Derivation Sketch

Let a wave operator be decomposed as
```
(L_b - V) ψ = s,
L_b ψ_inc = s,
L_b G(r,r') = δ(r-r')        with outgoing radiation condition.
```
Subtract the background equation:
```
L_b(ψ - ψ_inc) = V ψ.
```
Apply the background Green operator G=L_b^{-1}:
```
ψ = ψ_inc + G V ψ
ψ(r) = ψ_inc(r) + ∫_D G(r,r') V(r') ψ(r') dV'.
```
The sign of V depends on whether the contrast is written as L=L_b-V or
L=L_b+U; the physics is unchanged if the Green-function convention is kept
consistent.

## EM Volume Integral Equation

For a nonmagnetic inhomogeneous dielectric embedded in background
(ε_b, μ_b), with e^{-iωt} convention and dyadic Green function from
`electrodynamics: reasoning.em.dyadic_green_function`:
```
∇×∇×E - ω² μ_b ε_b E = iω μ_b J_ext + ω² μ_b (ε - ε_b) E.
```
Let E_inc be the field produced by J_ext in the homogeneous background, and let
G̿_b solve
```
∇×∇×G̿_b - k_b² G̿_b = I̿ δ(r-r'),     k_b²=ω² μ_b ε_b.
```
Then the electric-field VIE is
```
E(r) = E_inc(r)
     + ω² μ_b ∫_D G̿_b(r,r') · [ε(r') - ε_b] E(r') dV'.
```
Compact mnemonic: `E=E_inc+ω²μ_b∫G_b·(ε-ε_b)E dV`, with G_b understood as
the background dyadic Green operator for vector EM.
Equivalently, using polarization current/source
```
P(r)= [ε(r)-ε_b] E(r),
J_pol(r)= -iω P(r),
E = E_inc + ω² μ_b ∫ G̿_b · P dV'.
```
Because G̿_b has a source-region singularity, practical VIEs use principal-value
integration plus the depolarization/self term described in the dyadic Green node.

## Neumann Series, Born Approximation, and Rytov Note

In operator notation:
```
ψ = ψ_inc + G V ψ
(I - G V) ψ = ψ_inc.
```
If the scattering operator is small enough, ||GV||<1, invert by a Neumann series:
```
ψ = (I - GV)^(-1) ψ_inc
  = ψ_inc + GV ψ_inc + GVGV ψ_inc + GVGVGV ψ_inc + ... .
```

- Zeroth order: ψ≈ψ_inc.
- First Born approximation:
  ```
  ψ_scat(r) ≈ ∫ G(r,r') V(r') ψ_inc(r') dV'.
  ```
  The field inside the source term is replaced by the incident field.
- Higher Born terms add multiple scattering inside the contrast region.
- Rytov approximation: write ψ=ψ_inc exp(χ), solve approximately for the complex
  phase/log-amplitude χ. Rytov is often better than Born for predominantly
  forward, phase-accumulating propagation, but it still fails for caustics,
  zeros of ψ_inc, and strong multiple scattering.

## Discretization via Volume Method of Moments

Choose basis functions {u_n} in the contrast region D and write
```
E_h(r) = Σ_n e_n u_n(r),       Δε(r)=ε(r)-ε_b.
```
Galerkin testing with {w_m} gives
```
Σ_n [<w_m,u_n> - ω² μ_b <w_m, G̿_b · (Δε u_n)>] e_n = <w_m,E_inc>.
```
Matrix form:
```
A e = b,
A_mn = M_mn - K_mn,
M_mn = <w_m,u_n>,
K_mn = ω² μ_b ∫_D w_m*(r) · ∫_D G̿_b(r,r')·[Δε(r')u_n(r')] dV' dV,
b_m  = <w_m,E_inc>.
```
Common unknown choices:

- Total field E: direct VIE, contrast appears in the integral kernel.
- Polarization P=ΔεE: often improves material handling; equation becomes
  [Δε^{-1} - ω²μ_b G̿_b]P = E_inc, where Δε^{-1} is local.
- Susceptibility χ=(ε-ε_b)/ε_b: write E=E_inc+k_b²∫G̿_b·χE dV'.

The matrix is dense because every cell couples through G̿_b, but only the
scatterer volume is meshed. FFT/VIE accelerators, FMM, H-matrices, or low-rank
compression reduce matvec cost.

## Algorithm — Contrast Distribution → Scattered Field

```
1. DEFINE BACKGROUND:
   Pick ε_b, μ_b and the outgoing Green function G or G̿_b.
   Compute E_inc or ψ_inc in the background medium.

2. DEFINE CONTRAST REGION D:
   V(r) for scalar problems, or Δε(r)=ε(r)-ε_b for EM.
   Mesh only D, not the surrounding homogeneous space.

3. CHOOSE UNKNOWN AND BASIS:
   Scalar ψ, vector E, polarization P, acoustic pressure p, displacement u, etc.
   Choose voxel, tetrahedral, pulse, rooftop, SWG, or higher-order vector bases.

4. ASSEMBLE VIE:
   A = I - G V, or for EM A = M - ω² μ_b G̿_b Δε.
   Treat singular self cells with analytic extraction/PV depolarization terms.

5. SOLVE:
   Direct for small N; GMRES/BiCGStab for large dense systems.
   Use FFT convolution for uniform grids, FMM/H-matrix for unstructured grids.

6. POST-PROCESS:
   Total field inside D is the solved unknown.
   Scattered field anywhere outside D:
     ψ_scat(r)=∫_D G(r,r') V(r')ψ(r') dV'
     E_scat(r)=ω²μ_b∫_D G̿_b(r,r')·ΔεE(r') dV'.
   Check optical theorem / power balance when applicable.
```

## Cross-Domain Mapping Table

| Domain | Background operator L_b | Contrast V or source term | Lippmann-Schwinger form | Typical approximation/discretization |
|---|---|---|---|---|
| Electromagnetics | ∇×∇× - k_b² acting on E | ω²μ_b(ε-ε_b)E, plus μ contrast if magnetic | E=E_inc+ω²μ_b∫G̿_b·ΔεE dV | Volume MoM/VIE, DDA, FFT-VIE; Born/Rytov for weak dielectric contrast |
| Quantum scattering | E-H_0 or ∇²+k² | Potential U(r) with sign set by Schrödinger convention | ψ=φ+G_0 U ψ | Born series, T-matrix, partial waves, variational scattering |
| Acoustics | ∇²+k_b² for pressure p | Sound-speed/density contrast; effective potential V_ac p | p=p_inc+∫G_b V_ac p dV | Born/Rytov tomography, boundary/volume integral solvers |
| Elastic waves | Navier background operator | Density and Lamé-parameter contrasts coupling displacement components | u=u_inc+∫G̿_elastic · V_elastic u dV | Elastic VIE, seismic Born modeling, multiple-scattering solvers |
| Neutron/X-ray optics | Paraxial or Helmholtz background | Refractive-index/electron-density contrast | ψ=ψ_inc+∫G Vψ | Distorted-wave Born, phase/Rytov propagation |

## Edge Cases and Checks

- Strong resonant scatterers can make ||GV||≥1, so Born series diverges even
  though the exact integral equation remains solvable.
- High dielectric contrast requires accurate self terms; naive voxel collocation
  can give grid-dependent resonances.
- Open-region radiation is built into G. Do not add an artificial outer boundary
  unless using a hybrid FEM/VIE or domain-decomposition method.
- If the background is layered or periodic, replace free-space G̿_b by the
  corresponding Sommerfeld/periodic dyadic Green function.
- Magnetic contrast adds terms involving ∇×[(μ^{-1}-μ_b^{-1})∇×E], which are
  less local than the simple Δε source form and require compatible basis/testing.

## Cross-References

- electrodynamics: reasoning.em.dyadic_green_function (parent — G̿_b and singular self term)
- computational-physics: reasoning.cp.galerkin_rayleigh_ritz (Galerkin projection of VIE)
- computational-physics: reasoning.cp.moment_method (MoM matrix assembly)
- mathematics-theorems: mathematics.vector_green_identities (integral identities behind Green representation)
