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
---

# reasoning.cp.pml_absorbing_bc — Outgoing Wave → Absorbed in PML

## Core Picture

The Perfectly Matched Layer (PML) is an artificial absorbing material that,
in the continuous limit, produces ZERO reflection for waves at ANY frequency
and ANY incidence angle. It is realized by complex coordinate stretching:
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

## Comparison: CPML vs Split-Field PML vs UPML

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

## Cross-References

- Berenger, J. Comp. Phys. 114, 185 (1994) — original split-field PML
- Roden & Gedney, MOTL 27, 334 (2000) — CPML
- computational-physics: reasoning.cp.fdtd_yee_algorithm (parent)
- computational-physics: reasoning.cp.finite_element_method (PML truncation for FEM)
- mathematics-theorems: mathematics.sommerfeld_integral (PML as complex coordinate stretching in k-space)
