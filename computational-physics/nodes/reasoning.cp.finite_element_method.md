---
skill_id: reasoning.cp.finite_element_method
type: reasoning
summary_50t: >
  Weak form of ∇×μ⁻¹∇×E − k₀²ε_r E = −ik₀Z₀J. Expand E = Σ e_j N_j(r)
  with edge elements (Nédélec). Assemble [K−k₀²M][e]=[b]. Impose BCs.
  Solve sparse linear system. PML/ABC at truncation boundary.
  hp-adaptivity for accuracy. Complex symmetric (lossless) or general.
trigger:
  - frequency-domain EM in complex geometries (inhomogeneous, curved)
  - cavity/waveguide/discontinuity eigenanalysis, scattering from dielectrics
reasoning_role: fem_helmholtz_solver
parent: reasoning.em.uniqueness_theorem_boundary_value
retrieval_cost: 1
---

# reasoning.cp.finite_element_method — ∇×∇×E−k²E = f → [S][e] = [b]

## Core Picture

FEM solves the weak (variational) form of the vector Helmholtz equation on an
unstructured mesh. Edge elements (Nédélec, Whitney forms) ensure tangential
continuity of E across material interfaces while allowing normal discontinuity
— exactly what Maxwell requires. The result is a sparse linear system amenable
to direct or iterative solvers.

## Derivation Sketch

From `electrodynamics: reasoning.em.uniqueness_theorem_boundary_value`
(the BVP has a unique solution; FEM is the numerical method to find it):

The vector wave equation (curl-curl form):
```
∇×(μ_r⁻¹ ∇×E) − k₀² ε_r E = −i k₀ Z₀ J    in V
n̂×E = 0 on Γ_PEC,   n̂×∇×E = 0 on Γ_PMC
```

### Weak Form (Galerkin procedure)

1. Dot with test function W, integrate over V:
   ∫_V [∇×W·(μ_r⁻¹∇×E) − k₀² W·ε_r E] dV = −ik₀Z₀∫_V W·J dV
   (Boundary terms from integration by parts vanish if W satisfies BCs.)

2. Discretize: E(r) ≈ Σ_{j=1}^N e_j N_j(r) where N_j are vector edge basis
   functions. Each N_j has unit circulation along edge j and tangential
   continuity. This removes spurious (non-physical) modes.

3. Galerkin testing (W = N_i):
   Σ_j e_j [∫ ∇×N_i·μ_r⁻¹∇×N_j dV − k₀² ∫ N_i·ε_r N_j dV] = −ik₀Z₀∫ N_i·J dV

4. Matrix: [K]{e} − k₀²[M]{e} = {b}
   K_ij = ∫ ∇×N_i·μ_r⁻¹∇×N_j dV  (stiffness)
   M_ij = ∫ N_i·ε_r N_j dV         (mass)
   b_i = −ik₀Z₀∫ N_i·J dV         (excitation)

## Algorithm — Given Model → Mesh → Assemble → Solve

```
1. GEOMETRY + MESH: Create unstructured mesh (triangles in 2D, tetrahedra in 3D).
   Mesh must resolve λ: element size ≤ λ/(10-20). Refine near edges, corners,
   material interfaces.

2. CHOOSE ELEMENT ORDER:
   - p=1 (lowest-order Nédélec): 6 unknowns per tetrahedron (edges).
   - p=2: 20 unknowns per tetrahedron (edges + faces).
   Higher p = exponential convergence for smooth solutions (p-refinement).

3. ASSEMBLE SYSTEM:
   for each element:
     a. Compute local stiffness K^e and mass M^e via numerical quadrature
     b. Map to global indexing (sparse matrix assembly)
     c. Accumulate into global [K] and [M]

4. IMPOSE BOUNDARY CONDITIONS:
   - PEC: Zero out rows/cols for DoFs on Γ_PEC, set diagonal=1, RHS=0.
   - Port/waveguide: Modal expansion at port surface → Robin BC.
   - Radiation/ABC: PML layers or absorbing BC on outer boundary.

5. SOLVE: [K−k₀²M] {e} = {b}.
   - Direct: MUMPS, PARDISO (up to ~10⁶ unknowns)
   - Iterative: preconditioned CG/GMRES for larger problems
   - Eigenvalue: [K]{e} = k₀²[M]{e} for resonant cavities

6. POST-PROCESS: E(r) = Σ e_j N_j(r). Compute S-parameters from port
   coefficients, far-field from near-field transform surface.
```

## Edge Elements (Why Not Nodal?)

Nodal (scalar) elements at material interfaces force ALL E components continuous
— but Maxwell requires only TANGENTIAL E continuous. This produces spurious
(non-zero divergence) modes. Edge elements:
- Tangential continuity across faces ✓
- Normal discontinuity allowed ✓
- Discrete de Rham complex: grad → curl → div preserved exactly
- No spurious modes, no need for penalty terms

## Edge Cases

- **DC/Low frequency (k₀→0)**: The curl-curl matrix K becomes singular
  (gradient fields are in the null space). Solution: tree-cotree gauge or
  A-φ formulation.
- **High-contrast materials** (e.g., plasmonic metals at optical frequencies):
  ε_r negative → [K−k₀²M] indefinite. Use direct solvers or specialized
  preconditioners.
- **Unbounded problems**: PML is the standard truncation. Ensure PML thickness
  ≥ λ/4 and smooth conductivity profile to minimize artificial reflections.

## Cross-References

- Volakis, Chatterjee & Kempel (1998) Ch.2-4
- Zhu & Cangellaris (2006) Ch.1-3
- electrodynamics: reasoning.em.uniqueness_theorem_boundary_value (parent)
- computational-physics: reasoning.cp.multigrid_solver (fast sparse solve)
- computational-physics: reasoning.cp.pml_absorbing_bc (domain truncation)
