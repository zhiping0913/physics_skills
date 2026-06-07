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

## Variational Origin

For source current J and time convention e^{−iωt}, the curl-curl equation is
the stationary point δF = 0 of the electromagnetic functional
```
F(E) = 1/2 ∫_V [ μ⁻¹ |curl E|² − k² ε |E|² ] dV
       − Re ∫_V E · (iωJ) dV.
```
Taking the first variation and integrating the curl term by parts gives the
weak curl-curl operator plus a boundary term. Essential boundary condition:
n̂×E = 0 (PEC/tangential E prescribed). Natural boundary condition:
n̂×curl E = 0 (PMC/free boundary in the μ-normalized form).

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
   - PORT BC: (a) Pre-compute 2D port eigenmodes via separate FEM eigenvalue solve on the cross-section mesh. (b) At port surface Γ_p, enforce Robin BC: n̂×∇×E + γ n̂×(n̂×E) = U_inc, where γ = iβ_m for propagating mode m and U_inc is the incident modal field. (c) In the weak form, the boundary term is −∮_{Γ_p} γ (n̂×W)·(n̂×E) dS − ∮_{Γ_p} W·U_inc dS. (d) For multi-port problems, repeat per port; each port contributes independently to the system matrix and RHS.
   - PML IN FEM: In frequency-domain FEM, PML is implemented through complex anisotropic material tensors: ε̃ = ε Λ, μ̃ = μ Λ with Λ = diag(s_y s_z/s_x, s_z s_x/s_y, s_x s_y/s_z) and s_i = 1 + σ_i/(iωε₀). These substitute directly into K and M assembly — no auxiliary variables. The resulting system is complex symmetric: use GMRES, QMR, or direct (MUMPS) solvers. Caution: CG fails for complex symmetric matrices.

5. SOLVE: [K−k₀²M] {e} = {b}.
   - Direct: MUMPS, PARDISO (up to ~10⁶ unknowns)
   - Iterative: preconditioned CG/GMRES for larger problems
   - EIGENVALUE FOR CAVITIES: Solve [K]{e} = k₀²[M]{e}. Use ARPACK shift-invert: (K − σM)⁻¹ M x = λ x with σ = (2π f_target/c)². Request 2-3× the expected number of modes in the band to filter spurious ones. The inner solve (K − σM) y = M x at each Arnoldi iteration needs a direct sparse solver. For leaky modes (with PML), eigenvalues are complex; sort by |Im(λ)|.

6. POST-PROCESS: E(r) = Σ e_j N_j(r). S-PARAMETERS: Extract modal coefficients from the FEM field at each port using power orthogonality: a_m = ½ ∫_{Γ_p} (E×h_m* + e_m*×H)·n̂ dS. For port j excited: S_{ij} = b_i / a_j (all other ports matched). De-embed phase to reference plane if needed. Verify: Σ|S_{ij}|² ≤ 1 (passivity check).
```

## Edge Elements (Why Not Nodal?)

Nodal (scalar) elements at material interfaces force ALL E components continuous
— but Maxwell requires only TANGENTIAL E continuous. This produces spurious
(non-zero divergence) modes. Edge elements:
- Tangential continuity across faces ✓
- Normal discontinuity allowed ✓
- Discrete de Rham complex: grad → curl → div preserved exactly
- No spurious modes, no need for penalty terms

The discrete de Rham complex ensures Range(G) ⊆ Nullspace(K) where G is the discrete gradient (node→edge). For any nodal scalar φ, K·(G φ) = 0 exactly — gradient fields produce zero eigenvalue. Nodal elements break this: the discrete curl of a discrete gradient is non-zero, producing spurious non-zero eigenvalues in the curl-curl spectrum.

## Adaptive Refinement

Error indicator (residual-based): η_K = h_K ‖∇×μ⁻¹∇×E_h − k₀²εE_h − f‖_K + face jump terms ‖[n̂×μ⁻¹∇×E_h]‖_{∂K}. Mark elements where η_K > 0.5·max(η). Refine: smooth regions → p-refinement (exponential convergence); near corners/edges → h-refinement. Stop when global ‖η‖ < tolerance.

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
- computational-physics: reasoning.cp.absorbing_boundary_conditions (domain truncation)
