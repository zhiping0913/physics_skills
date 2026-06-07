---
skill_id: reasoning.em.dyadic_green_function
type: reasoning
summary_50t: >
  ∇×∇×G̿_e − k²G̿_e = I̿δ(r−r'). Free-space: G̿_e0 = (I̿ + ∇∇/k²) G₀
  where G₀ = e^{ikR}/(4πR). Classification: 1st kind (Dirichlet),
  2nd kind (Neumann), 3rd kind (mixed/interface). Eigenfunction expansion:
  complete L,M,N triad with L=∇ψ irrotational. Source-region singularity
  unified treatment: PV method with L̿ depolarization dyadic, spectral
  representation ΣL_nL_n*, equivalence tr(L̿)=1, cross-domain applications.
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

### 4. Eigenfunction Expansion — The Complete L,M,N Triad

Expand G̿_e in the complete orthonormal vector eigenfunctions {L_n, M_n, N_n}
of ∇×∇×, where L_n are IRROTATIONAL (∇×L_n=0, k-INDEPENDENT), while M_n, N_n
are SOLENOIDAL (∇·=0):

```
L_n = ∇ψ_n               (irrotational: ∇×L_n=0, ∇·L_n≠0)
M_n = ∇×[c_n ψ_n]        (solenoidal: ∇·M_n=0)
N_n = (1/k_n) ∇×M_n      (solenoidal, k_n eigenvalue of ∇×∇×)
```

where ψ_n satisfies the scalar Helmholtz equation (∇² + k_n²)ψ_n = 0, and c_n
is a piloting vector (often r or a constant unit vector) chosen to satisfy BCs.

The OHM-RAYLEIGH method: for source-free region, ∇×∇×E − k²E = 0, the solenoidal
part is spanned by {M_n,N_n}. But dyadic completeness demands including L_n:

```
I̿ δ(r−r') = Σ_n [L_n(r)L_n*(r') + M_n(r)M_n*(r') + N_n(r)N_n*(r')]
```

This is the DYADIC DIRAC DELTA IDENTITY. Applying ∇×∇× − k² to the Green's
dyadic expansion and using the eigenrelations ∇×∇×{M_n,N_n} = k_n²{M_n,N_n}:

```
G̿_e(r,r') = Σ_n [M_n(r)M_n*(r') + N_n(r)N_n*(r')] / (k² − k_n²)
```

Now the critical contribution from L_n: since ∇×∇×L_n = 0, the L_n term
solves ∇×∇×G̿_e = 0 in the eigenfunction expansion, but the DYADIC DELTA
IDENTITY forces its inclusion. Operating ∇×∇× − k² on the full expansion
(including L_n with eigenvalue 0 for ∇×∇×) gives:

```
G̿_e(r,r') = −(1/k²) n̂n̂ δ(R−R') + Σ_n (solenoidal expansion)
```

The δ-term — the SINGULARITY EXTRACTION — is UNIVERSAL for all geometries.
It originates from the discontinuity of G̿_m = ∇×G̿_e across the source, and
is essential for correct near-field evaluation in Method of Moments.

Why this matters: numerically, the eigenfunction series converges slowly
near r=r'. Extracting the δ-term and the closed-form G̿_e0 near-field
singularity enables accelerated MoM computations.

## Source-Region Singularity — Unified Treatment

### 5.1 Statement

Near the source point r≈r', G̿_e is a DISTRIBUTION, not a smooth function.
Its singular part is regularization-dependent: different exclusion volumes
(spherical, ellipsoidal, slab) produce different finite δ-term coefficients.
The general form (Chew §7.1):

```
G̿_e(r,r') = P.V. G̿_e(r,r') − (1/k²) L̿ δ(r−r')
```

where P.V. is the principal value defined by the chosen exclusion shape,
and L̿ is the DEPOLARIZATION DYADIC that encodes the shape's aspect ratios.
The physical field must be independent of the regularization — the
regularization-dependent L̿ precisely cancels the regularization-dependent
P.V. integral, yielding a unique total field.

### 5.2 Spatial Representation — PV Method (Chew §7.1.2)

The depolarization dyadic L̿ emerges from excluding an infinitesimal
ellipsoid centered at r=r'. For a general ellipsoid with semi-axes
(a,b,c) aligned along (x̂,ŷ,ẑ):

```
L̿ = L₁ x̂x̂ + L₂ ŷŷ + L₃ ẑẑ
```

where the DEPOLARIZATION FACTORS L_i are given by the elliptic integral:

```
L_i = (a b c / 2) ∫₀^∞ ds / [(s + s_i²) √((s+a²)(s+b²)(s+c²))]
```

with s₁=a², s₂=b², s₃=c². They satisfy the SUM RULE:

```
L₁ + L₂ + L₃ = 1   →   tr(L̿) = 1
```

**Special cases (all satisfy tr(L̿)=1):**

| Shape | Axes ratio | L̿ | Notes |
|-------|-----------|-----|-------|
| Sphere | a=b=c | L̿ = I̿/3 | Isotropic, each L_i=1/3 |
| Thin disk (⟂ ẑ) | a=b≫c | L̿ = ẑẑ | L₁≈0, L₂≈0, L₃≈1 |
| Needle (∥ x̂) | a≫b=c | L̿ = (ŷŷ+ẑẑ)/2 | L₁≈0, L₂=L₃≈1/2 |
| Slab (infinite in xy) | a,b→∞, c finite | L̿ varies | Depends on aspect ratio |

**Physical interpretation:** L̿ is the depolarization dyadic of a dielectric
ellipsoid of the same shape in electrostatics. The excluded volume's shape
determines how the singular self-field projects onto different directions.

### 5.3 Spectral Representation (Chew §7.3)

In the eigenfunction basis, the singular term arises from the IRROTATIONAL
(L) modes. Since ∇×L_n = 0, these modes have eigenvalue ZERO for ∇×∇×,
and in the dyadic Green's function expansion they contribute:

```
−(1/k²) Σ_n L_n(r) L_n*(r') = −(1/k²) n̂n̂ δ(r−r')
```

Key properties of L modes:
```
∇×L_n = 0           (irrotational — NO magnetic field coupling)
∇·L_n ≠ 0           (carries the longitudinal field)
L_n = ∇ψ_n          (gradient of scalar Helmholtz eigenfunction)
k-INDEPENDENT       (mode shape independent of wavenumber k)
```

The dyad n̂n̂ is the DIRECTION OF INTEGRATION ORDER: if the eigenfunction
sum is performed as a triple sum (e.g., in m,n,l indices for a rectangular
cavity), the order of summation determines n̂. For a SPHERICAL cavity sum
(r,θ,φ → summed radially last), n̂ = r̂ and n̂n̂ = r̂r̂.

**Connection to L̿:** In a cavity shaped to match the excluded volume
of the PV method, Σ L_n L_n* yields exactly L̿ δ(r−r').

### 5.4 Equivalence of Spatial and Spectral (Chew §7.1.4)

Both representations describe the SAME physics — the source-region
singularity of the dyadic Green's function. The equivalence rests on:

```
tr(L̿) = tr(n̂n̂) = 1
```

In free space (spherical exclusion), L̿ = I̿/3 and n̂n̂ = r̂r̂, both have
trace 1. The difference between L̿ and n̂n̂ is absorbed into the definition
of the P.V. integral and the summation convention:

```
P.V._sphere G̿_e − (I̿/3k²)δ = P.V._disk G̿_e − (ẑẑ/k²)δ = unique E(r)
```

The total field is INDEPENDENT of regularization — this is guaranteed
by the sum rule tr(L̿)=1 and the fact that the irrotational part
contributes −(1/k²)L̿ δ, exactly compensating the shape dependence of the
P.V. integral.

### 5.5 curl G̿ singularity and MFIE kernel

The magnetic dyadic Green function G̿_m = ∇×G̿_e has a weaker but still
non-integrable point singularity on a surface: curl G̿_e behaves like 1/R²
near R = |r−r'| → 0. Thus surface terms of the form

```
∫_S J_ms(r') · [∇×G̿_e(r,r')] dS'
```

must be interpreted as a Cauchy principal value when the observation point r
lies on S. This is exactly the magnetic-field integral equation (MFIE) kernel.
Taking the limiting value from either side of a smooth boundary produces the
standard jump term: the singular part contributes ±(1/2)J_s (sign set by the
normal and field convention), so the boundary equation contains the familiar
1/2 J_s term plus the principal-value MFIE operator.

### 5.6 Layered media M̿/N̿ decomposition

For planar layered media, Fourier transform in the transverse coordinates and
write the spectral dyadic Green function as TE-to-z and TM-to-z pieces:

```
G̿(k_x,k_y; z,z') = M̿ + N̿
M̿ = (∇×ẑ)(∇'×ẑ) F_TE
N̿ = (∇×∇×ẑ)(∇'×∇'×ẑ) F_TM / (iωε)
```

The scalar spectral kernels F_TE and F_TM carry the upward/downward propagation
factors and the generalized reflection/transmission coefficients of the layer
stack. This is the dyadic version of the Sommerfeld integral construction. In
anisotropic layered media the TE/TM channels generally couple; the independent
M̿/N̿ split is replaced by a 4×4 Berreman (first-order z-propagation) matrix.

### 5.7 Equivalence principle from magnetic currents J*,ρ*

The field-equivalence principle can be formulated by adding fictitious magnetic
current and magnetic charge to Maxwell's equations (for the e^{-iωt}
convention used here):

```
∇×E = iωμH − J*
∇×H = J − iωεE
∇·(εE) = ρ
∇·(μH) = ρ*
```

Stratton-Chu surface representations then replace the removed region by
equivalent surface currents. With the outward normal n̂ of the retained region,
one common convention is

```
J_s = n̂×H,
M_s = −n̂×E,
```

while authors using K* for magnetic current often write K* = n̂×E = −M_s.
Physically, the surface magnetic current encodes the discontinuity of the
tangential electric field: n̂×(E₂−E₁) = −M_s (up to the same sign convention).

### 5.8 Cross-Domain Applications

| Domain | Role of L̿ / δ-term | Key equation / concept |
|--------|---------------------|----------------------|
| **Dielectric ellipsoid** | Depolarization dyadic L̿ determines internal E for uniform external field | E_int = E_ext − L̿·P/ε₀ |
| **Clausius-Mossotti** | Spherical L̿=I̿/3 gives Lorentz local field correction | ε_eff = ε_b (1+2α)/(1−α), α molecular polarizability |
| **Lorentz field** | Spherical cavity exclusion; L̿=I̿/3 → E_loc = E + P/(3ε₀) | Classic dielectric local field |
| **Magnetized plasma ε̿** | Anisotropic ε̿ modifies L̿; G̿_e no longer (I̿+∇∇/k²)G₀ | Spectral-domain dyadic GF required |
| **MoM self-term** | Singularity extraction via L̿; self-patch integral closed-form | Z_mm = iωμ₀ ∫_patch ∫_patch f_m·G̿_e·f_m |
| **Kelvin cavity** | Needle-shaped (L̿=(ŷŷ+ẑẑ)/2) or disk-shaped (L̿=ẑẑ) exclusion | Historical debate resolved by L̿ shape choice |

**Key insight for Method of Moments:** The self-term (diagonal) of the
impedance matrix requires careful handling of the G̿_e singularity.
Subtracting the static singular kernel and using L̿ for the excluded
volume yields a convergent, regularization-independent result. For
RWG basis functions on triangular patches, the spherical exclusion
(L̿=I̿/3) is standard.

## Algorithm

```
1. Given the geometry and BCs, determine the dyadic wave equation for G̿_e.
2. If free-space: G̿_e0 = (I̿ + ∇∇/k²) G₀ (closed form).
      **Caveat**: If the medium is anisotropic (e.g., ε̿ tensor, magnetized plasma):
      the free-space decomposition G̿_e0 = (I̿+∇∇/k²)G₀ FAILS. Use the
      spectral-domain method: Fourier transform in transverse plane, solve
      the 4×4 system for each k_ρ, inverse FT. Cross-ref:
      `plasma.dielectric_tensor_magnetized`.
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

## Cross-Domain Bridges

| Domain | Dyadic G̿ | Key Application |
|--------|-----------|-----------------|
| Antenna/MoM | G̿_e (free-space or layered) | EFIE: E = iωμ₀∫G̿_e·J dV' → [Z][I]=[V] |
| Cavity/waveguide | G̿_e1 (1st kind, Dirichlet) | Resonator eigenmodes, coupling coefficients |
| Plasma (anisotropic) | ε⁻¹ in dyadic wave equation | Magnetized plasma has ε̿ anisotropic → G̿_e not (I̿+∇∇/k²)G₀ |
| Optics (layered) | G̿_e via Sommerfeld integrals | SPP Green's function, dipole emission near interface |
| Plasmonics | Spectral G̿_e(k_ρ) | Purcell factor, LDOS from Im[G̿_e] |

## Cross-References

- Tai, *Dyadic Green Functions in EM Theory* (1993) Ch.3-5, Ch.10
- Collin, *Field Theory of Guided Waves* (1990) Ch.2
- Chew, *Waves and Fields in Inhomogeneous Media* (1999) Ch.2, Ch.7
- electrodynamics: reasoning.em.green_function_poisson (parent — scalar G → dyadic G)
- mathematics-theorems: mathematics.dyadic_algebra (dyadic operations)
- mathematics-theorems: mathematics.vector_green_identities (dyadic Green's identity level)
