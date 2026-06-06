---
skill_id: reasoning.cp.fdtd_yee_algorithm
type: reasoning
summary_50t: >
  Discretize Maxwell's equations on staggered Yee grid. Explicit leapfrog
  time-stepping: E^{n+1}=E^n+(Δt/ε)∇×H^{n+½}, H^{n+½}=H^{n−½}−(Δt/μ)∇×E^n.
  Courant stability: Δt≤1/(c√(1/Δx²+1/Δy²+1/Δz²)). TF/SF source injection.
  Numerical dispersion: ω differs from ck for finite Δx. PML absorbs outgoing.
trigger:
  - broadband time-domain EM simulation in inhomogeneous media
  - pulse propagation, scattering, antenna radiation, PIC field solver
reasoning_role: time_domain_maxwell_solver
parent: reasoning.em.helmholtz_decomposition
retrieval_cost: 1
---

# reasoning.cp.fdtd_yee_algorithm — ∂_t(E,B) → Discrete Leapfrog

## Core Picture

The Finite-Difference Time-Domain (FDTD) method directly discretizes Faraday's
and Ampère's laws in time and space on a staggered grid (Yee 1966). E and H are
offset by half a cell spatially and half a time-step temporally, giving a fully
explicit, conditionally stable scheme that preserves the divergence constraints
∇·D = ρ, ∇·B = 0 automatically.

## Derivation Sketch

From `electrodynamics: reasoning.em.helmholtz_decomposition` (Maxwell as two
first-order curl equations):

Faraday:  ∂B/∂t = −∇×E − M_source
Ampère:   ∂D/∂t = ∇×H − J_source

### 1. Yee Grid Staggering

```
E_x at (i+½, j, k)      H_x at (i, j+½, k+½)
E_y at (i, j+½, k)      H_y at (i+½, j, k+½)
E_z at (i, j, k+½)      H_z at (i+½, j+½, k)
```

Each E component is surrounded by 4 circulating H components (and vice versa).
This naturally implements the integral form of the curl: ∮_C E·dl = −∂/∂t ∫ B·dS.

### 2. Discrete Curl

Central differences on the Yee grid (example: E_x component):
```
∂H_z/∂y ≈ [H_z(i+½,j+½,k) − H_z(i+½,j−½,k)] / Δy
∂H_y/∂z ≈ [H_y(i+½,j,k+½) − H_y(i+½,j,k−½)] / Δz
```

### 3. Leapfrog Time-Stepping

```
H^{n+½} = H^{n−½} − (Δt/μ) (∇×E)^n           (Faraday)
E^{n+1}  = E^n + (Δt/ε) [(∇×H)^{n+½} − σ E^n]  (Ampère + loss)
```
Second-order accurate in both space and time. Explicit: no matrix solve.

## Algorithm — Given Problem → Grid → Step → Extract

```
1. DEFINE GRID: Choose Δx, Δy, Δz. At least 10-20 cells per minimum wavelength.
   Δ ≤ λ_min / N_ppw where N_ppw ≥ 10 (typical). Smaller Δ = less dispersion.

2. CHOOSE Δt: Courant-Friedrichs-Lewy (CFL) stability:
   Δt ≤ 1 / (c √(1/Δx² + 1/Δy² + 1/Δz²))
   For cubic cells (Δx=Δy=Δz=Δ): Δt ≤ Δ/(c√3). Typical: use 0.95×CFL limit.

3. MATERIAL ASSIGNMENT: Assign ε_r, μ_r, σ to each cell face/edge.

   Dielectric interfaces: at cell faces on a material boundary, use
   ε_eff = (ε₁+ε₂)/2 for tangential E components. For discontinuous normal E
   (staggered grid handles automatically via differently-weighted H-curl
   stencils on either side of the interface).

4. SOURCE INJECTION (TF/SF): Split the computational domain:
   - Total-field (TF) region: contains scatterer + incident + scattered fields.
   - Scattered-field (SF) region: only scattered fields (toward PML boundary).
   At the TF/SF interface, add incident field to E on TF side, subtract H on SF side.

5. TIME LOOP (principal algorithm):
   for n = 1 to N_steps:
     a. Update H^{n+½} from E^n via Faraday's law (3 nested loops over grid)
     b. Apply H-source at TF/SF interface
     c. Update E^{n+1} from H^{n+½} via Ampère's law
     d. Apply E-source at TF/SF interface
     e. Apply PML absorbing BCs at outer boundaries
     f. Record outputs (near-field probes, far-field transform surfaces)

6. POST-PROCESS:
   - Near-to-far-field transform (NFFFT): integrate equivalent currents on a
     closed surface in the TF region → far-field radiation pattern.
   - Fourier transform of time-domain probe → S-parameters, RCS vs frequency.
```

## Key Numerical Properties

- **Grid dispersion**: Phase velocity v_p(θ,Δ) < c for propagation not aligned
  with grid axes. E.g., along diagonal: v_p/c ≈ 1 − (π²/12)(Δ/λ)².
  Mitigation: finer grid or higher-order schemes (FDTD(2,4)).
- **Staggered grid preserves ∇·B=0**: The discrete divergence of the curl is
  identically zero on the Yee grid. If ∇·B=0 initially, it stays zero forever.
- **Material interfaces**: ε and σ at E-nodes, μ at H-nodes. Averaging at
  interfaces required for accurate reflection/transmission.
- **Conformal FDTD**: For curved PEC surfaces, modify the Faraday contour
  integral for partially filled cells (Dey-Mittra algorithm).

## PEC BOUNDARIES

On the Yee grid, set E_tan = 0 on faces coinciding with PEC. Specifically:
for a PEC plane at x = x_0, zero out E_y and E_z on that face after each
E-update. H components at PEC faces: do NOT force to zero (they are
automatically tangential and emerge from the curl of adjacent E). Edge/corner:
zero both tangential components. Total energy diagnostic:
U = ½ Σ (ε|E|² + μ|H|²) should remain constant (σ=0, no PML); monitor to
<0.1% drift over full simulation.

## Edge Cases

- **Dispersive media**: ε(ω) not constant → use auxiliary differential equation
  (ADE) or recursive convolution. Drude, Debye, Lorentz models require extra
  time-marching equations for polarization current J_p.
  Debye example: ε(ω) = ε_∞ + Δε/(1+iωτ). Auxiliary equation:
  τ ∂P/∂t + P = ε₀ Δε E. Discrete: P^{n+1} = α P^n + β E^{n+½}
  with α = (2τ−Δt)/(2τ+Δt), β = 2ε₀Δε Δt/(2τ+Δt).
  Then D = ε₀ε_∞ E + P.
- **Thin layers (≪ Δx)**: Use subcell models or surface impedance BC.
- **Instability from PML**: Convolutional PML (CPML) more stable than split-field
  PML for long simulations and evanescent waves.

## SUBCELL MODELS

- **Thin wire** (radius a < Δx/2): Holland-Simpson model — modify the
  surrounding H-curl coefficients with ln(Δx/a) correction to the effective
  radius.
- **Thin slot**: use Babinet dual with magnetic current line source.
- **Conformal FDTD** (Dey-Mittra): for curved PEC surfaces crossing cell
  faces, adjust the Faraday contour integral with the fractional open area.

## Cross-References

- Yee, IEEE TAP 14, 302 (1966); Taflove & Hagness, *Computational Electrodynamics*
- Peterson, Ray & Mittra (1997) Ch.11-12
- electrodynamics: reasoning.em.helmholtz_decomposition (parent — continuous curl eqns)
- computational-physics: reasoning.cp.pml_absorbing_bc (PML truncation of FDTD grid)
- plasma: reasoning.plasma.laser_plasma_interaction (FDTD-PIC for laser-plasma)
