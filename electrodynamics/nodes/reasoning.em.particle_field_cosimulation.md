---
skill_id: reasoning.em.particle_field_cosimulation
type: reasoning
summary_50t: >
  Generic particle-field co-simulation skeleton: particle advance + force
  interpolation + field solve + current deposition = one timestep. Same
  cycle operates across plasma (Lorentz+Maxwell), astrophysics (gravity+
  Poisson), semiconductors (drift-diffusion+Poisson), molecular dynamics
  (spring potentials+direct sum). Hockney & Eastwood Ch.1-8 provide the
  canonical formulation. Domain specializations supply the force law, field
  equations, and boundary conditions.
trigger:
  - recognizing the same simulation cycle in any particle-based physics code
  - choosing between PM, PP, P3M force calculation strategies
  - understanding numerical errors shared across all particle methods
reasoning_role: particle_field_cosimulation
parent: reasoning.cp.fdtd_yee_algorithm
retrieval_cost: 1
sign_convention: >
  Δt = timestep. Δx = mesh spacing. N_p = number of particles.
  S(x) = shape function (interpolation kernel). Leap-frog: x^n, v^{n+1/2}.
  Force types: Lorentz (plasma), gravitational (astrophysics), spring
  (MD), drift-diffusion (semiconductor).
---

# reasoning.em.particle_field_cosimulation — Generic Skeleton

## Core Picture

A particle-field co-simulation advances two coupled representations in time:
(1) a collection of discrete macro-particles carrying mass, charge, momentum;
(2) continuous fields defined on a computational mesh. At each timestep, the
same five-step cycle operates regardless of physical domain: plasma,
astrophysical N-body, semiconductor device, or molecular dynamics. Only the
**force law** and **field equations** change between domains. This node
captures the universal skeleton; domain-specific nodes supply the physics
(Hockney & Eastwood 2020, Ch.1–8).

## Derivation Sketch

### 1. The universal simulation cycle

Every particle-field co-simulation executes:

```
① FIELD SOLVE:  L̂ f = ρ(x)         [solve for fields f from particle density ρ]
② FORCE GATHER: F_i = q_i G(x_i,f)  [interpolate force at particle positions]
③ PARTICLE PUSH: p_i → p_i + Δt F_i  [advance momentum; position advance follows]
④ CURRENT/DENSITY DEPOSIT: ρ(x) ← {x_i, v_i}  [accumulate back to mesh]
→ loop to ①
```

where L̂ is the field operator (∇² for Poisson, ∇× for Maxwell, etc.), and
G(x,f) is the force law (Lorentz, Newton gravity, spring potential).

### 2. Force calculation strategies (Hockney & Eastwood Ch.5,7,8)

Three fundamental approaches, in order of increasing accuracy and cost:

| Method | Force type | Complexity | Best for |
|--------|-----------|-----------|----------|
| **PM** (Particle-Mesh) | Mesh-mediated only | O(N_p + N_g log N_g) | Collisionless, large N_p |
| **PP** (Particle-Particle) | Direct pair summation | O(N_p²) | Strong collisions, few particles |
| **P3M** (PP+PM) | Short-range PP + long-range PM | O(N_p N_nb + N_g log N_g) | Mixed collisional/collisionless |

**PM (Particle-Mesh)**:
1. Deposit ρ(x) from particles to mesh using shape function S(x−x_i).
2. Solve field equation on mesh (FFT for Poisson, Yee for Maxwell).
3. Interpolate force ∇f back to particles using same S(x).

The shape function S(x) smooths the particle singularity. Common choices:
NGP (nearest grid point, zeroth order), CIC (cloud-in-cell, first order),
TSC (triangular-shaped cloud, second order). Higher order → smoother
fields, less noise, but more computational work.

**P3M (Particle-Particle Particle-Mesh)**:
- Short-range (r < r_cut): direct PP force, corrected for mesh smoothing.
- Long-range (r > r_cut): mesh-mediated PM force.
- The mesh supplies the "background" field, PP corrections add the
  correlations at small separations.

### 3. Time integration (Hockney & Eastwood Ch.4)

**Leap-frog** (second-order, symplectic, explicit):
```
v^{n+1/2} = v^{n-1/2} + (q Δt/m) F(x^n)
x^{n+1} = x^n + Δt v^{n+1/2}
```
Preserves phase-space volume exactly (Liouville theorem). No amplitude error
in periodic motion. CFL-limited: ω_p Δt < 2.

**Predictor-corrector**: higher order, allows larger timesteps, but adds
computational overhead. Used when accuracy demands exceed leap-frog.

### 4. Numerical heating and the finite particle number

With N_p macro-particles, the fluctuation level is ~1/√(N_p N_c) where N_c
is the number of cells. This "graininess" causes:

- **Numerical collisionality**: spurious two-body relaxation due to discrete
  particles, scaling as ~(N_D)^{-1} where N_D is the Debye number.
- **Grid heating**: when Δx > λ_D, the grid cannot resolve Debye shielding →
  artificial temperature increase. Requirement: Δx ≲ λ_D.

These are **universal** — they affect plasma PIC, N-body gravity, and MD
simulations identically. Only the physical scale (λ_D vs clustering radius
vs bond length) changes.

### 5. Domain specializations

| Domain | Force law F = | Field operator L̂ | ρ source | Node |
|--------|--------------|-------------------|----------|------|
| **Plasma (PIC)** | q(E + v×B) | ∇× Maxwell (Yee) | charge/current | lp.R18 |
| **Astrophysical N-body** | −G m_i Σ m_j r̂_ij/r² | ∇² Poisson | mass | — |
| **Semiconductor device** | μ ∇φ + D ∇n | ∇² Poisson | charge | — |
| **Molecular dynamics** | −∇V(r_ij) (Lennard-Jones, etc.) | — (direct sum) | — | — |
| **Vortex methods** | Γ (vortex velocity) | ∇² stream function | vorticity | — |

### 6. The shape function as the unifying concept

The shape function S(x) — how a macro-particle's attributes are smeared
onto the mesh — connects all particle methods:

- In PIC: S(x) determines charge/current deposition (Esirkepov, Villasenor-Buneman).
- In N-body: S(x) is the mass smoothing kernel for PM gravity.
- In vortex methods: S(x) controls vorticity distribution.

The same mathematical requirements hold across domains: S(x) must be
normalized (∫S dx = 1), have compact support, and preserve moments up to
the desired order. A Gaussian S(x) gives spectral accuracy but infinite
support → practical truncation.

## Algorithm — Given (force law, field operator, N_p, N_g) → Simulation Setup

```
1. CHOOSE force strategy:
   PM if collisionless (ν_c ≪ ω_p, or long-range only).
   P3M if close encounters matter (ν_c ≳ ω_p, gravothermal collapse).
   PP if N_p < 10⁴.

2. CHOOSE shape function:
   NGP: fastest, noisiest. CIC: good compromise. TSC: smooth, slower.

3. CHOOSE time integrator:
   Leap-frog: standard, CFL-limited.
   Boris: for magnetized plasma (exact E×B drift).
   RK4/Verlet: for MD.

4. CHECK resolution:
   PM: Δx < λ_D (plasma) or < softening length (N-body).
   Δt < CFL limit: Δt < min(2/ω_p, Δx/v_max).

5. VERIFY on known test case (two-stream, Jeans instability, harmonic oscillator).
```

## Edge Cases

- **Aliasing**: when particle density variation has k > k_nyq (Nyquist wavenumber),
  aliased power appears at lower k → spurious forces. Mitigated by higher-order
  S(x) or finer mesh.
- **Energy conservation**: leap-frog conserves energy to O(Δt²). For long
  simulations (>> 1/ω_p), energy drift may accumulate. Use symplectic integrators.
- **Load balancing**: particles may cluster → some processors overloaded.
  Domain decomposition or particle sorting needed.

## Cross-References

- Hockney & Eastwood, *Computer Simulation Using Particles* (2020), Ch.1–8
- Birdsall & Langdon, *Plasma Physics via Computer Simulation* (2018)
- computational-physics: reasoning.cp.fdtd_yee_algorithm (parent — field solver)
- laser-plasma: reasoning.lp.pic_methods_laser_plasma (plasma specialization — R18)
- computational-physics: reasoning.cp.moment_method (alternative: integral equations)
