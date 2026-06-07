---
skill_id: reasoning.cp.pml_absorbing_bc
type: reasoning
summary_50t: >
  Truncate unbounded domain with layers that absorb outgoing waves without
  reflection. Complex coordinate stretching: ∂/∂x̃ = (1/s_x)∂/∂x where
  s_x = 1 + σ_x/(iωε₀). Split-field PML (Berenger 1994) vs UPML (Sacks 1995)
  vs CPML (Roden & Gedney 2000). Convolutional PML for dispersive/evanescent.
trigger:
  - truncating FDTD/FEM computational domain for open-region problems
  - absorbing outgoing waves with minimal artificial reflection
reasoning_role: absorbing_boundary
parent: reasoning.cp.fdtd_yee_algorithm
retrieval_cost: 1
sign_convention: >
  Stretching: s_i(ω) = 1 + σ_i/(iωε₀) assumes e^{−iωt} time convention.
  σ_i in S/m, ε₀ in F/m. CPML recursive convolution assumes
  piecewise-constant field over Δt, same Δt as parent FDTD/FEM grid.
  For frequency-domain (FEM): UPML tensors are complex symmetric.
---

# reasoning.cp.absorbing_boundary_conditions — Absorbing Boundary Conditions

## A. Engquist-Majda (1977) / Mur (1981) — One-Way Wave Equation

The foundational local ABC emerges from factoring the wave operator. In 1D, the
wave equation ∂²_tt φ = c² ∂²_xx φ factors exactly:

```
(∂_t − c ∂_x)(∂_t + c ∂_x) φ = 0
```

Retaining only the right-going factor ∂_t φ + c ∂_x φ = 0 gives the exact
radiation condition. Its simplest discrete implementation at the right boundary
x = x_R is:

```
φ(x_R, n+1) = φ(x_R − Δx, n)    (s = c Δt/Δx = 1)
```

In 2D/3D, the outgoing condition is a pseudo-differential operator:

```
∂_t φ + c √(1 + ∂²_yy + ∂²_zz) φ = 0      (normal along x)
```

The square root is nonlocal. Engquist-Majda approximate it via Padé or
paraxial expansion:

```
√(1 − α²) ≈ 1 − ½ α²     (first-order paraxial)
```

where α² = −(∂²_yy + ∂²_zz)/∂²_tt. This yields the Mur first-order ABC:

```
∂²_tx φ + c ∂²_tt φ − (c/2) ∂²_yy φ = 0    (2D, normal to x)
```

**Reflection**: The reflection coefficient for the N-th order paraxial
approximation at incidence angle θ is:

```
R(θ) ≈ [(1 − cos θ)/(1 + cos θ)]^N
```

Normal incidence (θ=0): R=0. Grazing (θ→90°): R→1 unless N is large. In
practice, N=1 or 2 is used; higher orders become numerically unstable.

## B. Lindman (1975) — Rational Approximation of √

Lindman attacked the same pseudo-differential operator via rational
approximation of √(1 − α²) in the frequency domain. The idea: approximate
√(1 − α²) by a rational function R_P(α²) = P(α²)/Q(α²) where P and Q are
polynomials. This leads to:

```
∂_t φ + c R_P(α²) φ = 0
```

Implemented via auxiliary differential variables, yielding a system of
first-order equations local in time. Lindman's method is equivalent to a
Padé approximant of the square root; the Padé table for √(z) at z=1 gives
optimal rational approximations:

```
√(z) ≈ (p₀ + p₁ z + … + p_M z^M) / (1 + q₁ z + … + q_N z^N)
```

Higher-order Padé → lower reflection over wider angles, but more auxiliary
variables (and more memory). This approach prefigures the auxiliary
differential equation (ADE) formulation later used in PML implementations.

## C. Bayliss-Turkel (1980) — Annihilating Spherical Harmonics

For exterior problems in spherical coordinates, the exact radiating solution
has the asymptotic expansion (in 3D):

```
φ(r, θ, φ, t) ∼ (1/r) Σ_{i=0}^{∞} f_i(t − r/c, θ, φ) / r^i
```

Bayliss and Turkel constructed a sequence of annihilating operators:

```
L_i = ∂_r + (1/c) ∂_t + i/r
```

The m-th order operator is the product:

```
B_m = ∏_{i=1}^{m} L_i
```

Applied to φ, it annihilates the first m terms of the asymptotic expansion:

```
B_m φ = O(1/r^{2m+1})
```

Explicitly, B₁ = ∂_r + (1/c)∂_t + 1/r (the Sommerfeld radiation condition for
3D). B₂ = (∂_r + (1/c)∂_t + 1/r)(∂_r + (1/c)∂_t + 2/r). Higher m yields
greater accuracy at nearer boundaries, at the cost of higher spatial
derivatives.

**Key insight**: This provides an ABC that is exact to O(1/r^{2m+1}) for any
outgoing spherical wave, placing the boundary at finite distance r = R. The
connection to the Sommerfeld condition is direct: B₁ φ = 0 is the classical
radiation boundary condition.

## D. Liao (1984) — Multi-Angle Plane-Wave Fit

Liao's method constructs the ABC by fitting a set of plane waves at
pre-selected angles. Given K angles {θ_k}, the outgoing field at the
boundary is expressed as a linear combination of plane waves propagating
in those directions. The update at the boundary uses a convolution over
spatial points aligned along each angle:

```
φ(x_R, t + Δt) = Σ_{k=1}^{K} a_k φ(x_R − c Δt cos θ_k, t)
```

where weights a_k are determined by a least-squares fit or exact
interpolation. This is closely related to **mode matching**: if the
discrete angles correspond to the eigenspectrum of the interior problem,
Liao's method becomes exact for that discrete set. In practice, K = 3–5
angles often suffice for engineering accuracy.

**Advantages**: No higher derivatives; unconditionally stable at the
continuous level. **Disadvantage**: Nonlocal in space — requires field
values at non-grid-aligned interpolation points. The method connects
naturally to boundary integral formulations and Dirichlet-to-Neumann maps.

## E. Perfectly Matched Layer (PML)

The PML is an artificial absorbing material that, in the continuous limit,
produces ZERO reflection for waves at ANY frequency and ANY incidence angle. It is realized by complex coordinate stretching:
replace real coordinates with complex ones in the direction normal to the PML
interface.

## Derivation Sketch

From `computational-physics: reasoning.cp.fdtd_yee_algorithm` (FDTD grid
must be finite; need absorbing boundaries):

### 1. Complex Coordinate Stretching

Replace x → x̃ where:
```
∂/∂x̃ = (1/s_x) ∂/∂x,    s_x(ω) = 1 + σ_x/(iωε₀)
```
In the stretched coordinate, plane waves e^{ik_x x} become e^{ik_x x̃} = e^{ik_x x} · e^{−(σ_x k_x/ωε₀)x}.
The real part propagates; the imaginary part attenuates (ABSORBS).

### 2. Maxwell in Stretched Coordinates

Ampère's law in stretched space:
```
∇_s × H = −iωε₀ ε_r E,   where ∇_s = (1/s_x)∂/∂x x̂ + (1/s_y)∂/∂y ŷ + (1/s_z)∂/∂z ẑ
```

### 3. No-Reflection Theorem

At a planar interface between free space (s_x=s_y=s_z=1) and a PML region
(s_x≠1, s_y=s_z=1), the reflection coefficient for a plane wave is:
```
R = 0   for ALL θ, ω   (continuous limit)
```
This is the defining property of PML. In discrete implementation, residual
reflection ~ O(10⁻³) from finite layer thickness and discretization.

## Algorithm — Given FDTD/FEM Domain → Add PML → Simulate

```
1. PML THICKNESS: N_cells ≥ 8-10 cells. Thicker = lower reflection.
   Typical: 10 cells of PML → R ∼ 10⁻⁴ to 10⁻⁶.

2. CONDUCTIVITY PROFILE (polynomial grading):
   σ(ρ) = σ_max (ρ/d)^m   where ρ = distance into PML, d = PML thickness
   m = 3-4 (polynomial order). σ_max chosen for theoretical reflection:
   σ_max = −(m+1) ln[R(0)] / (2η₀ d)   where R(0) ≈ 10⁻⁴ is target reflection.

3. CHOOSE PML TYPE:
   a. UPML (uniaxial PML): Modify ε and μ as anisotropic tensors.
      ε̃ = ε Λ, μ̃ = μ Λ where Λ = diag(s_y s_z/s_x, s_z s_x/s_y, s_x s_y/s_z).
      Works in both FDTD and FEM. Preferred for frequency-domain.
   b. CPML (convolutional PML): Time-domain implementation of stretched
      coordinates via recursive convolution. MORE STABLE for long simulations,
      evanescent waves, and dispersive media. Standard choice for FDTD.

4. CPML IMPLEMENTATION (Gedney & Roden 2000):
   For each field component, store auxiliary convolution variables ψ_{E,xy}, etc.
   Update: E_x^{n+1} = E_x^n + (Δt/ε)[(∂H_z/∂y + ψ_{Exy}) − (∂H_y/∂z + ψ_{Exz})]
   ψ_{Exy}^{n+1} = b_y ψ_{Exy}^n + c_y (∂H_z/∂y)^{n+½}
   b_y = exp(−(σ_y + α_y)Δt/ε₀)
   c_y = σ_y (b_y − 1) / (σ_y + α_y)
   (With κ_y ≠ 1: b_y = exp(−(σ_y/κ_y + α_y)Δt/ε₀),
    c_y = σ_y(b_y−1)/(κ_y(σ_y + κ_y α_y)).)
   α_y: real pole shift for evanescent wave absorption (α_max ≈ 0.05–0.3).

5. CORNER REGIONS: PML in 2+ directions simultaneously. The overlapping
   σ_x and σ_y multiply → no special corner treatment needed for UPML/CPML.

6. VERIFICATION: Place a source, run, measure reflection from PML as
   |E_total − E_reference|/|E_reference|. Should be < 10⁻³.
```

## PML Sub-Comparison: CPML vs Split-Field PML vs UPML

| Type | Stability | Evanescent Absorption | Ease of Implementation | Used In |
|------|-----------|----------------------|----------------------|---------|
| Split-field (Berenger) | Poor for long runs | No | Moderate | Legacy FDTD |
| UPML | Good | No (κ=1 only) | Easy | FEM, freq-domain FDTD |
| CPML | Best | Yes (α_y term) | Moderate | Modern FDTD |

## Edge Cases

- **Grazing incidence (θ→90°)**: PML reflection increases. Mitigation: thicker
  PML, higher m, or CFS-PML (complex frequency shifted).
- **Late-time instability in split-field PML**: Well-documented for long
  simulations. Switch to CPML.
- **Dispersive media in PML**: The convolution must include the medium's
  dispersion. Use ADE-PML or direct integration of auxiliary equations.

## Comprehensive ABC Comparison

| Method | Reflection (normal) | Reflection (grazing) | Memory Overhead | Stability | Best Use Case |
|--------|---------------------|----------------------|-----------------|-----------|---------------|
| Engquist-Majda / Mur | 0 (exact for 1D) | ~[(1−cosθ)/(1+cosθ)]^N | Negligible | Unstable for N≥3 | Quick 2D FDTD, low-order |
| Lindman (Padé) | 0 | Depends on Padé order | ~N auxiliary vars | Stable | Frequency-domain, moderate accuracy |
| Bayliss-Turkel | O(R^{−2m−1}) | Exact at r→∞ | ~m derivative coeffs | Stable | Spherical exterior, FEM/BEM |
| Liao (multi-angle) | ~0 at fitted angles | Poor off design | ~K stored planes | Unstable for large K | Mode-matched problems, DtN maps |
| PML (UPML/CPML) | <10⁻⁴ (10 cells) | <10⁻³ (thick) | ~10-20 cells/layer | CPML: excellent | General-purpose FDTD/FEM |

**Guidance**: PML is the modern default for general electromagnetic/acoustic
truncation. Engquist-Majda/Mur remains useful for quick prototyping and
pedagogy. Bayliss-Turkel is preferred for spherical exterior problems
(formal error bounds). Liao excels when the outgoing field has known
directional composition. Lindman's rational approach is a theoretical
bridge between one-way wave equations and PML auxiliary variables.

## Cross-References

- Berenger, J. Comp. Phys. 114, 185 (1994) — original split-field PML
- Roden & Gedney, MOTL 27, 334 (2000) — CPML
- computational-physics: reasoning.cp.fdtd_yee_algorithm (parent)
- computational-physics: reasoning.cp.finite_element_method (PML truncation for FEM)
- mathematics-theorems: mathematics.sommerfeld_integral (PML as complex coordinate stretching in k-space)
