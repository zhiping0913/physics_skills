---
skill_id: reasoning.cp.dgtd_method
type: reasoning
summary_50t: >
  Discontinuous Galerkin Time Domain: Maxwell as hyperbolic conservation law
  ∂_t U + ∇·F(U) + S = 0. Element-local Galerkin with discontinuous basis.
  Inter-element coupling via Riemann upwind flux. Block-diagonal mass matrix
  → explicit time stepping (RK4 or leap-frog). CFL: Δt ≤ C·h_min/(c·(p+1)²).
  Cross-domain: CFD Godunov/Roe, MHD Riemann, DG-elasticity, DG-Schrödinger.
trigger:
  - time-domain EM on unstructured, non-conforming meshes with high-order accuracy
  - problems requiring hp-adaptivity without global mass matrix solves
  - multiphysics coupling (plasma, multiphase) via flux-based interface conditions
reasoning_role: dgtd_maxwell_solver
parent: reasoning.cp.galerkin_rayleigh_ritz
retrieval_cost: 1
---

# reasoning.cp.dgtd_method — Hyperbolic Conservation Law → Riemann Flux → Element-Local Time Marching

## Core Picture

DGTD is the time-domain version of the Discontinuous Galerkin method applied
to Maxwell's equations. It combines FEM's geometric flexibility (unstructured
meshes, curved elements) with FVTD's flux-based inter-element communication.
The key insight: Maxwell's equations are a hyperbolic conservation law, and
element coupling is handled by solving a Riemann problem at each interface —
the same mathematical framework that unifies CFD, MHD, and seismic wave
simulation.

## Derivation Sketch

From `computational-physics: reasoning.cp.galerkin_rayleigh_ritz` (variational
Galerkin projection) and `computational-physics: reasoning.cp.finite_element_method`
(element-local weak form), extended to time-domain with discontinuous basis:

### 1. Maxwell as hyperbolic conservation law

```
∂_t U + ∇·F(U) + S = 0

U = (E_x, E_y, E_z, H_x, H_y, H_z)ᵀ     (state vector, 6 components)
F(U) = flux tensor with components from ∇×E = −μ ∂_t H, ∇×H = ε ∂_t E + J
S = source vector (impressed currents J)
```

The flux Jacobian matrix Ǎ = n̂·∂F/∂U has eigenvalues: ±c, 0 (×4), where
c = 1/√(με). The two non-zero eigenvalues correspond to the two
characteristic waves crossing the interface in opposite directions — the
physical basis for the upwind flux.

### 2. Element-local weak form

On each element Ω_i, expand the field in a local basis {Λ_k(r)}:
```
U_h(r,t) = Σ_k u_k^i(t) Λ_k(r)    (independent in each element)
```

Galerkin weak form with integration by parts:
```
∫_{Ω_i} Λ_k · ∂_t U_h dV − ∫_{Ω_i} (∇×Λ_k) · F(U_h) dV
  + ∮_{∂Ω_i} Λ_k · [n̂×F*(U_h)] dS = −∫ Λ_k · S dV
```

The surface integral introduces the **numerical flux** F*, which couples
neighboring elements. Because the basis is discontinuous across element
boundaries, the flux at an interface must be defined from the left and right
states (U⁻, U⁺) — this is the Riemann problem.

### 3. Riemann problem → upwind flux (Kast eq 4.19-4.20)

At each interface with normal n̂ (pointing from element i to j):
```
n̂×H* = n̂×[(Z_i H_i + Z_j H_j) + n̂×(E_i − E_j)] / (Z_i + Z_j)
n̂×E* = n̂×[(Y_i E_i + Y_j E_j) − n̂×(H_i − H_j)] / (Y_i + Y_j)
```
where Z_i = √(μ_i/ε_i) is the wave impedance, Y_i = 1/Z_i.

This upwind flux is derived from the Rankine-Hugoniot jump conditions across
a propagating electromagnetic discontinuity. It is the Maxwell-equation
analog of the Roe flux in CFD. Alternative: centered flux (arithmetic mean of
interface values — no dissipation but potentially unstable for long runs).

### 4. Semi-discrete system and time integration

After spatial discretization:
```
M_i ∂_t u_i = R_i(u_i, u_neighbors)
```
where M_i is the **element-local block-diagonal mass matrix**. Because the
basis is discontinuous, M_i couples only DOFs within element i — a K×K matrix
that can be pre-inverted once per element.

**Time integration options**:
- **RK4** (Kast eq 4.27): 4-stage, 4th-order explicit. Standard choice.
- **Leap-frog** (Kast eq 4.30-4.31): Staggered E/H time levels, 2nd-order.
  Requires electric and magnetic fields at staggered sub-time levels.

**CFL condition**:
```
Δt ≤ C · h_min / (c · (p+1)²)
```
where h_min is the minimum element size, p is the polynomial order, and C is
a scheme-dependent constant (C ≈ 0.2-0.4 for typical DGTD).

### 5. Boundary conditions via flux modification

- **PEC**: set E⁻ = −E⁺, H⁻ = H⁺ in the flux formula (mirror E, keep H)
- **PMC**: set H⁻ = −H⁺, E⁻ = E⁺ in the flux formula (dual)
- **Silver-Müller ABC** (Kast eq 4.32-4.33): set exterior state to zero;
  flux reduces to impedance-matched outgoing condition
- **PML**: apply complex coordinate stretching in element-local material
  matrices; absorbing without reflection in principle

### 6. DGTD-plasma multiphysics (D32)

Kast §5.3 demonstrates DGTD coupled to plasma fluid equations for modeling
high-power microwave (HPM) air breakdown. The coupling enters through:
- J_plasma = −e n_e v_e (plasma current in Maxwell source term S)
- v_e from momentum equation ∂_t v_e = −(e/m_e)E − ν_c v_e
- n_e from continuity equation with ionization rate ν_i(E)

This is directly relevant to laser-plasma interaction where the electromagnetic
pulse ionizes the medium and then interacts with the resulting plasma.

## Algorithm — Mesh → Semi-Discrete System → Time March

```
1. MESH: Generate unstructured mesh (triangles/tetrahedra). Elements may be
   non-conforming — hanging nodes are allowed.

2. CHOOSE BASIS: Select polynomial order p per element (p-adaptivity).
   Typical: Lagrange nodal basis of degree p on each element.

3. PRE-COMPUTE per element:
   - Mass matrix M_i^E, M_i^H (block-diagonal, K×K each)
   - Stiffness matrix S_i (curl operator on element)
   - Surface-to-volume mapping for each face
   - Invert mass matrices: M_i^{-1} stored for fast time stepping

4. TIME LOOP (n = 0, 1, ...):
   a. For each element face: compute Riemann flux F* from (U_i, U_j).
   b. Assemble RHS: R_i = S_i u_i + Σ_faces M_surface · F* − source term
   c. Update: u_i^{n+1} = u_i^n + Δt M_i^{-1} R_i (RK4 substep)

5. POST-PROCESS: Extract fields on sampling points/surfaces. Far-field
   via near-to-far-field transformation on a Huygens surface.
```

## DGTD vs FEM vs FDTD

| Property | FEM (frequency-domain) | FDTD (Yee) | DGTD |
|----------|----------------------|------------|------|
| Mesh | Unstructured, conforming | Structured Cartesian | Unstructured, non-conforming OK |
| Mass matrix | Coupled (global sparse) | Diagonal (implicit) | Block-diagonal (element-local) |
| Time stepping | Implicit or explicit | Explicit (leap-frog) | Explicit (RK4 or leap-frog) |
| Polynomial order | Up to p ≈ 3-4 practical | p = 2 (spatial) | High-order p-adaptive |
| Adaptivity | h-refinement | Subgridding (hard) | h-/p-adaptivity element-local |
| Flux at interfaces | Continuity enforced | Automatic (staggered) | Riemann/upwind flux |
| Multiphysics coupling | Via source terms | Via auxiliary equations | Flux-based + source terms |

## Cross-Domain Template — Riemann/Upwind Flux

The same Rankine-Hugoniot framework appears across hyperbolic PDEs:

| Domain | Conservation Law | Riemann Solver |
|--------|-----------------|----------------|
| CEM (DGTD-Maxwell) | ∂_t(E,H) + ∇×(...) = 0 | Upwind flux from Maxwell eigenvalues ±c |
| CFD (Euler) | ∂_t(ρ,ρu,ρE) + ∇·F = 0 | Godunov / Roe / HLLC flux |
| MHD | ∂_t(ρ,ρu,B,E_tot) + ∇·F = 0 | MHD Riemann solver (fast/slow magnetosonic + Alfvén) |
| DG-elasticity | ∂_t(σ,v) + ∇·F = 0 | Upwind flux from P/S wave speeds |
| DG-Schrödinger | iℏ ∂_t ψ = Hψ | Numerical flux from quantum hydrodynamic form |

**Unifying principle**: any first-order hyperbolic system admits a DG
discretization with numerical flux derived from the characteristic
decomposition of the flux Jacobian.

## Application to Laser-Plasma Problems

- **HPM air breakdown**: DGTD-plasma coupling for modeling laser/ microwave
  pulse propagation through ionizing atmosphere.
- **Laser-induced plasma filamentation**: DGTD captures the sharp plasma
  gradients and field enhancement at filament boundaries via unstructured,
  adaptive meshing.
- **Alternative to PIC in fluid-plasma regimes**: When kinetic effects are
  subdominant, DGTD + cold/warm plasma fluid model provides a computationally
  efficient alternative to full PIC.

Cross-reference: `plasma: reasoning.plasma.laser_plasma_interaction`

## Edge Cases

- **Centered flux instability**: The non-dissipative centered flux can
  accumulate spurious modes. Always prefer upwind flux for long simulations.
- **CFL with high p**: The (p+1)² factor makes high-order DGTD very
  restrictive on time step. Local time stepping or implicit-explicit (IMEX)
  schemes mitigate this.
- **Dielectric interfaces**: The Riemann flux handles impedance mismatch
  automatically through Z_i, Z_j — no special treatment needed.
- **Dispersive media**: Extend state vector U to include polarization/
  magnetization auxiliary variables (ADE method, same as FDTD).

## Cross-References

- Kast, J., et al., *Advanced Time Domain Modeling for EM* (2022) Ch.4-5
- Hesthaven, J.S., Warburton, T., *Nodal Discontinuous Galerkin Methods* (2007)
  — the canonical DG textbook
- Cockburn, B., Shu, C.W., "TVB Runge-Kutta local projection discontinuous
  Galerkin" J. Comput. Phys. (1989) — foundational DG-CFD paper
- Bourdel, F., et al., first DG-Maxwell formulation (1991)
- computational-physics: reasoning.cp.galerkin_rayleigh_ritz (parent — DG is
  Galerkin with discontinuous basis)
- computational-physics: reasoning.cp.finite_element_method (conforming sibling)
- computational-physics: reasoning.cp.fdtd_yee_algorithm (structured grid alternative)
- plasma: reasoning.plasma.laser_plasma_interaction (plasma physics context)
