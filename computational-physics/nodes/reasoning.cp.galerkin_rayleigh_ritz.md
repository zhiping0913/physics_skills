---
skill_id: reasoning.cp.galerkin_rayleigh_ritz
type: reasoning
summary_50t: >
  Variational/Rayleigh-Ritz/Galerkin unification: for self-adjoint L, stationarity
  of F(u)=<u,Lu>-2Re<u,f> gives Lu=f. Expanding u_h=Σα_n u_n yields
  Aα=b with A_mn=<u_m,Lu_n>. Galerkin testing with w_i=u_i gives the same
  system; specializations include MoM, volume IE, FEM, and modal bases.
trigger:
  - recognizing when FEM, MoM, modal expansion, and Rayleigh-Ritz are the same projection idea
  - deriving a matrix system from a weak/variational form
  - choosing basis/test functions for computational physics solvers
reasoning_role: variational_galerkin_unifier
parent: mathematics.vector_green_identities
retrieval_cost: 1
---

# reasoning.cp.galerkin_rayleigh_ritz — δF=0 ⇔ Aα=b ⇔ Galerkin residual orthogonality

## Core Picture

Rayleigh-Ritz, Galerkin FEM, and many Method-of-Moments formulations are the
same projection principle viewed through different languages:

- Variational language: make a quadratic functional stationary.
- Galerkin language: force the residual to be orthogonal to a finite test space.
- Matrix language: assemble A_mn=<test_m, L basis_n> and solve Aα=b.

The bridge to `mathematics-theorems: mathematics.vector_green_identities` is
integration by parts / Green's identities: they move derivatives between trial
and test functions, expose boundary terms, and convert a strong equation Lu=f
into a weak or integral equation.

## Derivation Sketch

Let H be a complex Hilbert space with inner product <v,u> anti-linear in v and
linear in u. Let L be self-adjoint on the chosen domain, with boundary conditions
that make the surface terms from Green's identity vanish or become natural BCs.

### 1. Variational principle for a driven linear problem

For
```
L u = f
```
define the real functional
```
F(u) = <u, L u> - 2 Re <u, f> .
```
Perturb u → u + ε δu. Using self-adjointness, <u,Lδu>=<Lu,δu>=<δu,Lu>*:
```
δF = 2 Re <δu, L u - f> .
```
If variations δu span the admissible space, then
```
δF = 0 for all δu    ⇔    L u = f.
```
Thus Rayleigh-Ritz for a source problem is simply stationarity of the energy-like
quadratic functional.

Compact mnemonic: `F(u)=<u,Lu>-2Re<u,f>`, `δF=0⇔Lu=f`, and
`u_h=Σα_nu_n -> Aα=b`; Galerkin with `w_i=u_i` gives the same matrix.

### 2. Rayleigh-Ritz finite-dimensional subspace

Choose trial functions {u_n}_{n=1}^N satisfying the essential boundary conditions:
```
u_h(r) = Σ_{n=1}^N α_n u_n(r).
```
Insert into F:
```
F(α) = α† A α - 2 Re(α† b)
A_mn = <u_m, L u_n>
b_m  = <u_m, f>.
```
Stationarity with respect to α_m* gives
```
∂F/∂α* = A α - b = 0    ⇒    A α = b.
```
For self-adjoint positive L, A is Hermitian positive definite after constraints;
for Helmholtz/curl-curl problems A is often Hermitian indefinite or complex
symmetric depending on loss and convention.

### 3. Galerkin residual orthogonality gives the same equations

Define the residual
```
R_h = L u_h - f.
```
Weighted residual methods impose
```
<w_i, R_h> = 0,    i=1,...,N.
```
The Galerkin choice is `w_i = u_i`, so
```
0 = <u_i, L Σ_n α_n u_n - f>
  = Σ_n <u_i, L u_n> α_n - <u_i, f>
```
and therefore
```
A α = b
```
with the same A and b as Rayleigh-Ritz. Petrov-Galerkin is the non-identical
trial/test generalization w_i ≠ u_i; point matching is w_i=δ(r-r_i).

### 4. Eigenvalue Rayleigh-Ritz as the homogeneous version

For eigenproblems
```
L u = λ M u
```
the Rayleigh quotient is
```
ρ[u] = <u,L u> / <u,M u>.
```
Expanding in the same basis yields the generalized matrix eigenproblem
```
A α = λ B α,
A_mn=<u_m,L u_n>,   B_mn=<u_m,M u_n>.
```
Modal expansion is the special case where {u_n} are known eigenmodes, often
making A or B diagonal.

## Algorithm — Strong/Integral Equation → Projection Matrix

```
1. IDENTIFY OPERATOR:
   Write the physics as L u = f, or L u = λ M u for an eigenproblem.
   Decide the inner product: volume, surface, weighted material inner product,
   or power/energy inner product.

2. APPLY GREEN'S IDENTITY:
   Move derivatives from u to test functions to obtain a weak form.
   Boundary terms become:
     - essential constraints imposed on basis functions, or
     - natural boundary terms added to the bilinear form/RHS.

3. CHOOSE TRIAL SPACE:
   u_h = Σ α_n u_n.
   Pick basis functions that encode geometry, continuity, and singular behavior:
     - edge basis for curl problems,
     - RWG for surface currents,
     - cell/pulse basis for volume contrast,
     - analytic eigenmodes when available.

4. CHOOSE TESTING:
   Galerkin: w_i=u_i gives symmetry/Hermiticity when L is self-adjoint.
   Petrov-Galerkin: w_i chosen for stability/upwinding/non-self-adjoint L.
   Collocation: w_i=δ(r-r_i) gives point matching.

5. ASSEMBLE:
   A_in = <w_i, L u_n>,   b_i=<w_i,f>.
   For eigenproblems assemble A and mass/overlap matrix B.

6. SOLVE AND VERIFY:
   Solve Aα=b or Aα=λBα. Check residual norm, energy balance, boundary
   conditions, convergence under h/p/basis enrichment, and symmetry/reciprocity.
```

## Specializations in Computational Electromagnetics

| Method | Unknown u | Trial/test basis | Operator L / kernel | Matrix entries | Why it is Galerkin/Ritz |
|---|---|---|---|---|---|
| Surface MoM for PEC/dielectric surfaces | Surface current J_s, sometimes magnetic current M_s | RWG edge functions on triangular surface mesh; Galerkin tests often same RWG | Dyadic Green kernel G̿_e/G̿_m in EFIE, MFIE, CFIE, PMCHWT | Z_mn=∫_S f_m·∫_S G̿·f_n dS' dS plus scalar-potential/divergence terms | Residual of boundary integral equation is orthogonal to current basis space |
| Volume MoM / VIE | Volume field E or polarization P=(ε-ε_b)E | Voxel/tetrahedron pulse, rooftop, SWG, or vector basis functions | Lippmann-Schwinger volume integral with background dyadic Green G̿_b | A_mn=<w_m, u_n - ω²μ_b G̿_b Δε u_n> | Galerkin projection of contrast-scattering integral equation |
| FEM curl-curl | Electric field E, magnetic field H, or potentials | Nédélec/Whitney edge elements; sometimes higher-order hierarchical elements | Differential curl-curl: ∇×μ⁻¹∇×E - ω²εE | K_mn=∫(∇×N_m)·μ⁻¹(∇×N_n)dV, M_mn=∫N_m·εN_n dV | Weak form from integration by parts; Galerkin testing with same edge functions |
| Modal expansion | Coefficients of known modes | Eigenmodes of cavity/waveguide/free-space vector harmonics | Diagonal or nearly diagonal spectral operator | A_mn≈(λ_n-λ)δ_mn plus coupling terms | Rayleigh-Ritz in an eigenbasis; truncation gives best approximation in modal subspace |

## Cross-Domain Unification Table

| Domain | Functional / weak object | Trial space | Matrix problem | Physical meaning |
|---|---|---|---|---|---|
| Quantum Rayleigh-Ritz | Energy expectation E[ψ]=<ψ,Hψ>/<ψ,ψ> | Atomic orbitals, plane waves, finite elements, configuration basis | H c = E S c | Variational upper bounds for bound-state energies; configuration interaction is Galerkin in many-body basis |
| Solid mechanics FEM | Potential Π(u)=1/2∫ε(u):C:ε(u)dV - ∫u·f dV - ∮u·t dS | Nodal or vector displacement shape functions | K d = F | Stationary elastic potential energy; stiffness matrix from strain-displacement bilinear form |
| **Probability space (UQ)** | **⟨ψ_β, L Σ c_α ψ_α⟩_p = ⟨ψ_β, f⟩_p** | **Wiener-Askey orthogonal polynomials (Hermite, Legendre, Jacobi, Laguerre)** | **A c = b with A_{βα}=⟨ψ_β, L ψ_α⟩_p** | **Galerkin projection on probability Hilbert space — PCE, stochastic collocation. Same Aα=b structure as FEM/MoM but inner product is w.r.t. input PDF (cf. reasoning.cp.uncertainty_quantification)** |
| Ideal MHD stability | δW[ξ] from displacement ξ | Fourier harmonics, finite elements, flux-coordinate basis | K ξ = ω² M ξ or δW sign test | δW>0 stable; δW<0 instability. Green's identities expose surface terms and jump conditions |
| Acoustics | ∫(∇p·∇q* - k²pq*)dV - boundary terms | Nodal FEM, boundary elements, modes | (K-k²M)p=b | Pressure Helmholtz weak form / boundary integral projection |
| Heat/diffusion | ∫∇v·κ∇u dV - ∫vf dV | FEM nodal functions | K u = f | Minimum dissipation / weak Poisson equation |
| **Time domain (TDIE/MOT)** | **∫ w_m(r) · [L_t J](r,t) dS, causal L_t** | **RWG spatial × temporal basis T_j(t)** | **Z₀ α^i = V^i − Σ Z_{i−k} α^k (upper-triangular in time)** | **Space-time Galerkin with causality. MOT is time-domain block-upper-triangular Galerkin (cf. moment_method §TD extension)** |

## Edge Cases and Checks

- Self-adjointness is boundary-condition dependent: forgetting a boundary term can
  destroy Hermiticity and break the Rayleigh-Ritz equivalence.
- Loss, radiation conditions, convection, and open-region PMLs generally make the
  operator non-Hermitian; Galerkin still works, but the stationary real functional
  may not exist without adjoint/complex variational machinery.
- Essential BCs must be built into the trial space; natural BCs appear from the
  surface term after integration by parts.
- A singular basis self-term in MoM is not a failure of Galerkin; it requires
  principal-value integration, singularity extraction, or analytic self terms.

## Cross-References

- mathematics-theorems: mathematics.vector_green_identities (parent — weak forms from Green identities)
- computational-physics: reasoning.cp.moment_method (surface MoM projection)
- computational-physics: reasoning.cp.finite_element_method (Nédélec Galerkin FEM)
- computational-physics: reasoning.cp.modal_expansion_numerical (spectral/Rayleigh-Ritz truncation)
- computational-physics: reasoning.cp.lippmann_schwinger (volume integral equation Galerkin projection)
