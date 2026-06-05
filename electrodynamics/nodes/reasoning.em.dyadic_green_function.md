---
skill_id: reasoning.em.dyadic_green_function
type: reasoning
summary_50t: >
  ∇×∇×G̿_e − k²G̿_e = I̿δ(r−r'). Free-space: G̿_e0 = (I̿ + ∇∇/k²) G₀
  where G₀ = e^{ikR}/(4πR). Classification: 1st kind (Dirichlet),
  2nd kind (Neumann), 3rd kind (mixed/interface). Eigenfunction expansion:
  G̿_e = −(1/k²)n̂n̂ δ(R−R') + Σ (solenoidal series). G̿_m = ∇×G̿_e solenoidal.
trigger:
  - constructing EM field from arbitrary current sources
  - integral equation formulation (EFIE/MFIE), Method of Moments
  - cavity/waveguide/resonator dyadic Green's functions
reasoning_role: dyadic_green_em
parent: reasoning.em.green_function_poisson
retrieval_cost: 1
---

# reasoning.em.dyadic_green_function — I̿δ → G̿_e, G̿_m

## Core Picture

The electric dyadic Green's function G̿_e(r,r') gives the vector electric field
produced by a point current source: E(r) = iωμ₀ ∫ G̿_e(r,r')·J(r') dV'. It
satisfies the dyadic Helmholtz equation and is the foundation of integral
equation methods in electromagnetics (Tai 1993, Ch.4; Collin 1990, Ch.2).

## Derivation Sketch

Starting from `electrodynamics: reasoning.em.green_function_poisson` (scalar
Green's function G₀ = e^{ikR}/(4πR) for ∇²G₀ + k²G₀ = −δ):

### 1. Dyadic Wave Equation

From Maxwell: ∇×∇×E − k²E = iωμ₀J. The corresponding dyadic equation:
```
∇×∇×G̿_e(r,r') − k² G̿_e(r,r') = I̿ δ(r−r')
```
The magnetic dyadic Green's function: G̿_m(r,r') = ∇×G̿_e(r,r').

### 2. Free-Space Solution (closed form)

Using the scalar Green's function G₀:
```
G̿_e0(r,r') = (I̿ + ∇∇/k²) G₀(r,r')
```
where ∇∇ differentiates with respect to observation point r.
Explicitly (R = |r−r'|):
```
G̿_e0 = [I̿ (1 + i/kR − 1/k²R²) − R̂R̂ (1 + 3i/kR − 3/k²R²)] G₀
```
In the far zone (kR ≫ 1): G̿_e0 ≈ (I̿ − R̂R̂) G₀. This is the TRANSVERSE
dyadic — only the components perpendicular to R̂ survive.

Key identity: G̿_e0 is NOT solenoidal — ∇·G̿_e0 = −(1/k²)∇δ(r−r').

### 3. Classification by Boundary Conditions

| Kind | Name | BC on G̿_e | Physical meaning |
|------|------|-----------|-----------------|
| 1st | Dirichlet | n̂×G̿_e1 = 0 on S | PEC cavity/waveguide |
| 2nd | Neumann | n̂×∇×G̿_e2 = 0 on S | PMC boundary |
| 3rd | Mixed | Continuity of n̂×G̿_e and n̂×∇×G̿_e/μ | Interface between media |

For each kind: G̿_e = G̿_e0 + G̿_es where G̿_es is the scattering part
(homogeneous solution that satisfies the BC).

### 4. Eigenfunction Expansion — The Singular Term

Expand G̿_e in solenoidal (∇·=0) eigenfunctions {M_n, N_n} of ∇×∇×:
```
G̿_e(r,r') = Σ_n [M_n(r)M_n*(r') + N_n(r)N_n*(r')] / (k² − k_n²)
```
Including the IRROTATIONAL modes (L_n = ∇φ_n/k_n) reveals the critical term:
```
G̿_e(r,r') = −(1/k²) n̂n̂ δ(R−R') + Σ_n (solenoidal expansion)
```
The δ-term — the SINGULARITY EXTRACTION — is UNIVERSAL for all geometries.
It originates from the discontinuity of G̿_m = ∇×G̿_e across the source, and
is essential for correct near-field evaluation in Method of Moments.

Why this matters: numerically, the eigenfunction series converges slowly
near r=r'. Extracting the δ-term and the closed-form G̿_e0 near-field
singularity enables accelerated MoM computations.

## Algorithm

```
1. Given the geometry and BCs, determine the dyadic wave equation for G̿_e.
2. If free-space: G̿_e0 = (I̿ + ∇∇/k²) G₀ (closed form).
3. If bounded (cavity/waveguide/layered):
   a. Decompose: G̿_e = G̿_e0 (free-space part) + G̿_es (scattering part).
   b. Construct G̿_es to satisfy BCs using eigenfunction expansion or
      Sommerfeld integrals (for layered media).
   c. Include the singular term −(1/k²)n̂n̂δ(R−R') in the eigenfunction series.
4. E-field: E(r) = iωμ₀ ∫_V G̿_e(r,r')·J(r') dV' + surface terms.
5. H-field: H(r) = ∫_V G̿_m(r,r')·J(r') dV' where G̿_m = ∇×G̿_e.
```

## Key Properties

- **Symmetry**: G̿_e(r,r') = [G̿_e(r',r)]^T (reciprocity).
  G̿_m(r,r') = [G̿_m(r',r)]^T.
- **Solenoidal vs. non-solenoidal**: G̿_m is always solenoidal (∇·G̿_m = 0).
  G̿_e is NOT solenoidal due to the longitudinal source term.
- **Radiation condition**: For r→∞, G̿_e ~ outgoing waves (Sommerfeld).
- **Ohm-Rayleigh method**: G̿_e constructed from G̿_m via ∇×G̿_m = I̿δ + k²G̿_e.

## Edge Cases

- **Source coincides with observation (r=r')**: The free-space G̿_e0 contains
  a 1/R³ singularity. Principal value integration needed in MoM. Method:
  singularity subtraction — subtract the static (k→0) singular part G̿_static,
  integrate it analytically, add back.
- **Layered media**: G̿_e expressed via Sommerfeld integrals in k_ρ; branch
  cuts from √(k_i²−k_ρ²) require careful Riemann sheet selection.
- **Low frequency (k→0)**: G̿_e0 ~ (I̿−3R̂R̂)/(4πk²R³) singularly diverges.
  Use low-frequency decomposition (Helmholtz decomposition into irrotational
  + solenoidal parts).

## Cross-References

- Tai, *Dyadic Green Functions in EM Theory* (1993) Ch.3-5, Ch.10
- Collin, *Field Theory of Guided Waves* (1990) Ch.2
- Chew, *Waves and Fields in Inhomogeneous Media* (1999) Ch.2, Ch.7
- electrodynamics: reasoning.em.green_function_poisson (parent — scalar G → dyadic G)
- mathematics-theorems: mathematics.dyadic_algebra (dyadic operations)
- mathematics-theorems: mathematics.vector_green_identities (dyadic Green's identity level)
