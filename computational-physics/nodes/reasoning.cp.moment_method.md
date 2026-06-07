---
skill_id: reasoning.cp.moment_method
type: reasoning
summary_50t: >
  Lu=f → expand u=Σα_n u_n, test with w_m → [Z][α]=[V].
  Basis functions: pulse, triangle, RWG. Testing: point-matching, Galerkin.
  EFIE for PEC: n̂×E_scat = −n̂×E_inc. MFIE alternate. Matrix fill cost
  O(N²); FMM reduces to O(N log N). Condition number ∝ 1/(Δx).
trigger:
  - solving EM scattering/radiation from arbitrary conductor/dielectric bodies
  - integral equation formulation for antenna, RCS, EMC problems
reasoning_role: integral_equation_solver
parent: reasoning.em.dyadic_green_function
retrieval_cost: 1
---

# reasoning.cp.moment_method — L u = f → [Z][α] = [V]

## Core Picture

The Method of Moments converts a linear operator equation L u = f (integral or
differential) into a matrix equation by expanding the unknown u in basis functions
and testing with weight functions. In CEM, L is the electric/magnetic field integral
equation, u is the surface current, and f is the incident field.

## Derivation Sketch

From `electrodynamics: reasoning.em.dyadic_green_function` (dyadic G̿_e maps
source J to field E), the EFIE for a PEC scatterer:

```
n̂ × E_inc(r) = −n̂ × [iωμ₀ ∫_S G̿_e(r,r') · J(r') dS']   for r on S
```

This is L J = f with L being the integral operator. The MoM discretizes it:

1. **Expand**: J(r) ≈ Σ_{n=1}^N α_n f_n(r)  where {f_n} are basis functions
   defined on the mesh (pulse, RWG, rooftop).
2. **Test**: Take inner product with weight functions {w_m}:
   ⟨w_m, L J⟩ = ⟨w_m, f⟩ → Σ_n α_n ⟨w_m, L f_n⟩ = ⟨w_m, f⟩
3. **Matrix**: Z_{mn} = ⟨w_m, L f_n⟩,  V_m = ⟨w_m, f_inc⟩.
4. **Solve**: [Z][α] = [V] → α = Z⁻¹ V. Typically O(N³) direct or O(N²) iterative.

Galerkin: w_m = f_m (same as basis). Point-matching: w_m = δ(r−r_m).

## Algorithm — Given Geometry → Matrix → Current → Field

```
1. MESH: Discretize surface S into N patches/elements (triangles for 3D,
   segments for wires). Record node coordinates, connectivity, edge lengths.

2. CHOOSE BASIS: Select basis functions {f_n} defined on the mesh.
   - Wire: pulse, triangle, piecewise sinusoid
   - Surface (3D PEC): RWG (Rao-Wilton-Glisson) — each edge n:
     f_n(r) = (ℓ_n/(2A_n^±)) (r − r_n^±)  on triangle T_n^±; 0 elsewhere.
     RWG ensures ∇_s·J continuity — no artificial surface charge.

   For thin wires (radius a ≪ λ): use the reduced 1D EFIE with kernel
   K(z,z') = e^{−ikR}/R where R = √(a²+(z−z')²). The approximate kernel
   e^{−ik|z−z'|}/|z−z'| is valid when |z−z'| ≫ a.

3. CHOOSE TESTING: Galerkin (w_m = f_m) gives symmetric matrix for PEC.
   Point-matching faster but less accurate near edges.

4. FILL Z-MATRIX: For each m,n:
   Z_{mn} = iωμ₀ ∫_{S_m} f_m(r) · [∫_{S_n} G̿_e(r,r') · f_n(r') dS'] dS
          + (1/iωε₀) ∫_{S_m} (∇_s·f_m)(r) [∫_{S_n} G₀(r,r') (∇'_s·f_n)(r') dS'] dS
   The second term (scalar potential) handles the ∇∇/k² part of G̿_e.
   Cost: O(N²). Singularity when m=n → analytical extraction of 1/R singularity.

5. FILL EXCITATION: V_m = ∫_{S_m} f_m(r) · E_inc(r) dS.

6. SOLVE: [Z][α] = [V]. For large N (>10⁴): use iterative solver (GMRES, CG)
   with MLFMA (multilevel fast multipole) for O(N log N) matrix-vector products.

   PRECONDITIONING: For iterative solvers, use diagonal (P = diag(Z)⁻¹)
   for well-conditioned systems, block-diagonal for multi-scale geometries,
   or incomplete LU for general cases. Without preconditioning, CG/GMRES
   convergence stalls as N grows.

7. POST-PROCESS: J(s) = Σ α_n f_n(s). Far-field: E_ff(θ,φ) = −iωμ₀ (I̿−R̂R̂) · ∫ J e^{−ik·r'} dS' / (4πR). Near-field: evaluate E(r_near) = iωμ₀ ∫ G̿_e(r_near,r')·J(r') dS'. Use adaptive quadrature for observation points close to the surface. For r_near within λ/2π of surface → singularity extraction + numerical integration of the regular part.
```

## Equation Choices

| Problem | Equation | Kernel | Unknown | Notes |
|---------|----------|--------|---------|-------|
| PEC scatterer | EFIE | G̿_e | J_s | Valid for closed AND open surfaces |
| PEC scatterer (closed) | MFIE | n̂×G̿_m | J_s | Better conditioned for large smooth bodies |
| PEC (closed, resonance) | CFIE = α EFIE + (1−α)η MFIE | — | J_s | Removes interior resonance problem |
| Dielectric body | PMCHWT | G̿_e + G̿_m | J_s, M_s | Both electric and magnetic currents |
| Thin wire | Reduced EFIE | G₀ (scalar) | I(z) | 1D integral; use thin-wire kernel |

## For the Plasma Physicist: MoM ↔ PIC

MoM solves the frequency-domain integral equation for currents on surfaces —
the complement to time-domain PIC which tracks particles in volume. Plasma
applications: antenna coupling to plasma, RF heating launcher design, SPP
scattering from nanoparticles. Cross-ref: `plasma: reasoning.plasma.laser_plasma_interaction`.

## Surface vs Volume Integral Equations

- **Surface IE specialization**: EFIE/MFIE/CFIE reduce Maxwell scattering to
  equivalent currents on material boundaries. For PEC, EFIE solves only the
  electric surface current J_s. For dielectric penetrable bodies, PMCHWT uses
  both equivalent electric and magnetic currents (J_s, M_s) and enforces
  tangential E/H continuity across the interface.
- **Volume IE / Lippmann-Schwinger**: In an inhomogeneous volume embedded in a
  homogeneous background (ε_b, μ_b), the unknown is the total interior field:
  ```
  E(r) = E_inc(r) + ω² μ_b ∫_V G̿_b(r,r') · [ε(r') − ε_b] E(r') dV'
  ```
  This is the electromagnetic Lippmann-Schwinger equation; the contrast
  current is J_c = −iω[ε−ε_b]E. The **Born approximation** is the first
  Neumann iterate: replace E under the integral by E_inc.
- **Port/network MoM and S-matrix**: With modal port excitations, outgoing and
  incident wave amplitudes obey [V⁻] = [S][V⁺]. S is symmetric for reciprocal
  structures and unitary for lossless matched networks. In a power-normalized
  impedance basis, S = (Z−U)(Z+U)⁻¹, where U is the identity matrix.

## Edge Cases

- **Interior resonance**: EFIE/MFIE errors grow rapidly as k approaches an
  interior cavity eigenvalue k_res of the closed surface; condition number and
  current amplitude can show sharp spikes. Use CFIE when k > k_res/2 for the
  lowest relevant interior resonance, or scan frequency for spikes in cond(Z)
  and switch formulations near them. Fredholm alternative: MFIE uniqueness
  fails at interior resonances because the homogeneous integral equation has a
  nontrivial solution.
- **Low frequency (k→0)**: EFIE matrix becomes ill-conditioned (∇·J term
  dominates). Use the surface Helmholtz/Hodge split
  J_s = ∇_s φ + n̂×∇_s ψ (plus harmonic topology terms): the ∇_s φ part is
  longitudinal/charge-carrying and the n̂×∇_s ψ part is solenoidal/loop-like.
  Loop-star or loop-tree decompositions are discrete versions of this split.
  Without the split, the low-k EFIE mostly recovers ∇_s·J_s through the scalar
  potential term while the divergence-free current is poorly scaled and easily
  lost/contaminated.
- **Thin layer**: when thickness ≪ λ, use impedance BC instead of volumetric MoM.

## Cross-References

- Harrington, *Field Computation by Moment Methods* (1993) Ch.1-4
- Peterson, Ray & Mittra (1997) Ch.3-10
- electrodynamics: reasoning.em.dyadic_green_function (parent — G̿_e is the EFIE kernel)
- computational-physics: reasoning.cp.lippmann_schwinger (volume IE and Born/Neumann series)
- mathematics-theorems: mathematics.dyadic_algebra (RWG basis → dyadic products)
- mathematics-theorems: mathematics.vector_green_identities (EFIE from dyadic Green's identity)
