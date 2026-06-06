---
skill_id: reasoning.cp.multigrid_solver
type: reasoning
summary_50t: >
  Hierarchical solver: smooth high-frequency error on fine grid, restrict
  residual to coarse grid, solve coarse correction, prolong back.
  V-cycle: fine→coarse→fine. O(N) complexity for sparse linear systems.
  Curl-curl operator: Hiptmair hybrid smoother (distributive Gauss-Seidel
  on nodes + edges). Application to FEM [K−k₀²M]{e}={b}.
trigger:
  - solving large sparse FEM/MoM linear systems efficiently
  - eigenvalue problems requiring many matrix-vector products
reasoning_role: multilevel_iterative_solver
parent: reasoning.cp.finite_element_method
retrieval_cost: 1
---

# reasoning.cp.multigrid_solver — Sparse Ax=b → O(N) via Hierarchy

## Core Picture

Multigrid accelerates iterative solvers by attacking error at all scales
simultaneously. Standard iterative methods (Gauss-Seidel, Jacobi) quickly
smooth high-frequency error but stall on low-frequency (long-wavelength)
components. Multigrid projects the problem onto a hierarchy of coarser
grids where "low frequency on fine" becomes "high frequency on coarse."

## Derivation Sketch

From `computational-physics: reasoning.cp.finite_element_method` (the
FEM system [K−k₀²M]{e} = {b} is large, sparse, ill-conditioned):

1. **Error equation**: For approximate solution {ẽ}, residual {r} = {b} − [A]{ẽ}.
   The error {e_exact} = {ẽ} + {δ} satisfies [A]{δ} = {r}.
2. On a coarse grid (2× coarser), the long-wavelength error {δ} can be
   represented with fewer unknowns and solved cheaply.
3. The coarse correction {δ_c} is interpolated (prolongated) back to the fine
   grid and added: {ẽ_new} = {ẽ} + P {δ_c}.

## Algorithm — V-Cycle

```
function V_CYCLE(level ℓ, A_ℓ, b_ℓ, x_ℓ):
    if ℓ == coarsest:
        return A_ℓ⁻¹ b_ℓ    # direct solve on coarsest grid

    # Pre-smoothing: reduce high-frequency error
    x_ℓ = SMOOTH(A_ℓ, b_ℓ, x_ℓ, ν₁ steps)    # ν₁ = 2-3 Gauss-Seidel sweeps

    # Restrict residual to coarse grid
    r_ℓ = b_ℓ − A_ℓ x_ℓ
    r_{ℓ+1} = R r_ℓ          # R = restriction operator (injection or full-weighting)

    # Coarse-grid correction (recursive)
    δ_{ℓ+1} = V_CYCLE(ℓ+1, A_{ℓ+1}, r_{ℓ+1}, 0)

    # Prolongate correction to fine grid
    x_ℓ = x_ℓ + P δ_{ℓ+1}    # P = prolongation operator (linear interpolation)

    # Post-smoothing
    x_ℓ = SMOOTH(A_ℓ, b_ℓ, x_ℓ, ν₂ steps)   # ν₂ = 2-3 sweeps

    return x_ℓ
```

Grid hierarchy: finest (level 0) → coarsen by factor 2 → level 1 → ... → level L
(typically L=3-6 levels). Coarse matrices built by Galerkin: A_{ℓ+1} = R A_ℓ P.

## Curl-Curl Systems: Hiptmair Smoother

The curl-curl operator ∇×μ⁻¹∇× has a large null space (gradient fields).
Standard Gauss-Seidel fails because it cannot reduce error in the null space.

Hiptmair hybrid smoother (Zhu & Cangellaris §5):
1. **Distributive relaxation**: Transform to block-diagonal form.
2. Smooth on node space (scalar potential corrections) AND edge space (vector).
3. One hybrid sweep = one scalar Gauss-Seidel on nodes + one vector Gauss-Seidel
   on edges.

## Convergence Rate

Ideal multigrid (smooth problem, Poisson): error reduced by factor ~0.1 per
V-cycle, independent of mesh size → O(N) total solution time.
For curl-curl at high k₀: convergence degrades. Use shifted Laplacian
preconditioning or complex-shifted PML for exterior problems.

## Edge Cases

- **High wavenumber (k₀ large)**: The Helmholtz operator becomes indefinite.
  Standard multigrid fails (coarse grid cannot represent oscillatory solutions).
  Use complex-shifted preconditioner or switch to direct solver.
- **Strongly anisotropic mesh**: Semi-coarsening (coarsen in one direction only).
- **Non-nested grids**: Algebraic multigrid (AMG) constructs coarse spaces
  from matrix entries, not geometry.

## Cross-References

- Zhu & Cangellaris (2006) Ch.3-5
- Briggs, Henson & McCormick, *A Multigrid Tutorial*
- computational-physics: reasoning.cp.finite_element_method (parent — FEM matrix)
