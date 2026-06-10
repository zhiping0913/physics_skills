---
skill_id: reasoning.lp.pic_methods_laser_plasma
type: reasoning
summary_50t: >
  Particle-in-Cell (PIC) for laser-plasma: leap-frog integrator + Yee
  FDTD Maxwell solver → self-consistent kinetic simulation. Charge
  conservation (Esirkepov or Villasenor-Buneman). Boosted frame: Lorentz
  transform → γ_b² reduction in computational cost. QED modules: Monte
  Carlo photon emission + pair production. Ionization: ADK tunnel
  ionization, barrier suppression (BSI). Resolution: Δx ≲ λ_D, Δt <
c Δt < Δx/√d (CFL). Standard for LWFA, TNSA, RPA, QED-plasma modeling.
For 1D: Δt = Δx/c gives zero numerical dispersion (magic time-step, Taflove §2.6.2).
For 3D Yee: Δt = Δx/(c√3) minimizes numerical dispersion.
trigger:
  - setting up PIC simulation parameters (resolution, box size, #particles)
  - choosing between lab-frame vs boosted-frame PIC
  - understanding numerical artifacts (grid heating, numerical Cherenkov)
reasoning_role: pic_methods
parent: reasoning.cp.fdtd_yee_algorithm
retrieval_cost: 1
sign_convention: >
  Leap-frog: x at t_n, v at t_{n+1/2}, E/B at t_{n±1/2} (staggered).
  Yee mesh: E on edges, B on faces. CFL: cΔt < Δx/√d.
  Boosted frame: γ_b along laser direction. QED MC: probabilistic
  emission/absorption events per timestep.
---

# reasoning.lp.pic_methods_laser_plasma — Leap-Frog + Yee → Self-Consistent Kinetic

## Core Picture

Particle-in-Cell (PIC) simulation is the workhorse numerical method for
laser-plasma interaction. It tracks macro-particles (representing many
real electrons/ions) moving in self-consistent electromagnetic fields
computed on a grid via Maxwell's equations. The method is fully kinetic
— it resolves collisionless plasma dynamics including wave-particle
interactions, non-Maxwellian distributions, and kinetic instabilities.
For laser-plasma problems (LWFA, TNSA, RPA, QED cascades), PIC provides
first-principles predictions where fluid models fail (Birdsall & Langdon,
Macchi §9, Pukhov 2003).

## Derivation Sketch

### 1. PIC algorithm cycle

Each timestep (Δt):
```
① FIELD SOLVE:  ∇×E = −∂B/∂t,  ∇×B = μ₀ J + c⁻²∂E/∂t   [Yee FDTD]
② FIELD GATHER: E_i, B_i at particle positions (interpolation)
③ PARTICLE PUSH: dp/dt = q(E + v×B), dx/dt = v          [Boris/leap-frog]
④ CURRENT DEPOSIT: particle velocities → J on grid       [charge-conserving]
→ loop to ①
```

**Leap-frog integration** (2nd order, symplectic):
```
v^{n+1/2} = v^{n-1/2} + (qΔt/m) (E^n + v^n × B^n)
x^{n+1} = x^n + Δt v^{n+1/2}
```

**Boris pusher**: separates electric and magnetic rotation for stability.
Exact energy conservation for E×B drift (no numerical damping).

### 2. Yee FDTD for Maxwell's equations

Yee mesh (staggered grid):
- E_x at (i+1/2, j) edges, B_z at (i+1/2, j+1/2) face center.
- Automatic ∇·B = 0 to machine precision.
- 2nd-order central differences in space and time.

CFL condition (3D):
```
c Δt < 1 / √(1/Δx² + 1/Δy² + 1/Δz²)
c Δt < Δx/√3    [for cubic grid Δx = Δy = Δz]
```
For λ₀ = 0.8 μm resolved at Δx = λ₀/40 = 20 nm: Δt < 0.04 fs.

### 3. Charge conservation

The continuity equation ∇·J + ∂ρ/∂t = 0 must be satisfied numerically
to avoid spurious electrostatic fields. Two standard methods:

**Esirkepov method** (2001): current deposition from particle trajectories,
exactly conservative for any shape function. Widely used in PIC codes
(EPOCH, PIConGPU, OSIRIS).

**Villasenor-Buneman** (1992): analytic current decomposition. Simple,
exact, but limited to 1st-order shape functions.

Without charge-conserving current deposition, ∇·E = ρ/ε₀ is enforced
by Poisson correction (add electrostatic field → 4x cost).

### 4. Numerical stability requirements

| Parameter | Condition | Physical meaning |
|-----------|----------|-----------------|
| Δx | < λ_D (Debye length) | Resolve electrostatic shielding |
| Δx | < λ₀/N (N~20-40) | Resolve laser wavelength |
| Δt | < 2/ω_p | Resolve plasma oscillations |
| Δt | < Δx/c√d | CFL condition |
| N_particles/cell | > 10 | Reduce numerical noise |
| N_particles/Debye sphere | > 10 | Suppress numerical collisionality (universal: plasma, galaxies, MD) |
| Simulation time | > ω_pi⁻¹ | Capture ion dynamics |

**Numerical heating**: insufficient spatial resolution → self-heating.
Grid heating temperature: T_grid ∝ (Δx/λ_D)² × particle energy. Must keep
Δx ≲ 0.5 λ_D (strict) or 1 λ_D (moderate).

### 5. Boosted frame PIC

Laser-plasma simulations involve two disparate scales:
- Laser wavelength λ₀ ~ 1 μm
- Acceleration length L_acc ~ mm–cm
Ratio: L_acc/λ₀ ~ 10⁴–10⁵ — impossible in lab frame!

**Lorentz boost** along laser propagation direction:
```
γ_b = (1 + β_b²)^{-1/2} ≈ ω₀/ω_p    [optimal boost factor]
```
In the boosted frame:
- Laser wavelength: λ' = λ₀ / γ_b(1+β_b) ≈ λ₀ / (2γ_b)
- Plasma length: L' = L / γ_b
- Total speedup: γ_b² (one factor from shorter length, one from longer timestep)

For n_e = 10¹⁸ cm⁻³, γ_b ≈ 43 → speedup ~ 1800. 1 mm of plasma resolved at
λ₀/20 → grid from 500M cells to ~300k cells.

**Limitation**: numerical Cherenkov instability in boosted frame → requires
specialized solvers (PSATD, FFT-based).

### 6. Additional physics modules

**Ionization**: ADK (Ammosov-Delone-Krainov) tunnel ionization rate:
```
W_ADK ∝ exp(−2(2|E_i|)^{3/2} / 3|E|)    [atomic units]
```
BSI (Barrier Suppression Ionization): instantaneous when E > E_crit.

**Ionization regime boundary** (Keldysh parameter):
```
γ_K = ω √(2 I_p) / E₀    [Keldysh 1965]
γ_K ≫ 1: multiphoton ionization   γ_K ≪ 1: tunnel ionization
```
The laser-plasma skill assumes pre-formed plasma. For the detailed
atomic strong-field physics of the gas-to-plasma transition
(Keldysh parameter, ATI spectra, recollision), see the
`ultrafast-optics` skill (HHG/attosecond nodes) and Gavrila (1992).

**Collisions**: binary collision model (Nanbu, Takizuka-Abe) for ν_ei.
Pair-wise scattering with conservation. Monte Carlo.

**QED**: for χ_e > 0.01 — Monte Carlo photon emission (nonlinear Compton)
+ pair production (Breit-Wheeler). Photon emission probability per timestep
from QED differential rate. Photon and pair particles tracked as additional
species.

## Algorithm — Setting Up a PIC Simulation

```
1. PROBLEM SCALE: compute λ₀, λ_p, λ_D, L_acc, ω_pi⁻¹.
   Choose Δx = min(λ_D/2, λ₀/30), Δt = min(0.9·CFL, 0.2·2π/ω_p).

2. BOX SIZE: L_box > L_acc + margins for boundaries.
   Transverse: > few × w₀ (laser spot) for LWFA.
   For TNSA: target thickness ~μm, vacuum gap ~10 μm.

3. N_PARTICLES: N_pcell > 10 for electrons, > 4 for ions.
   Total macroparticles ~ 10⁶–10⁹.

4. BOOSTED FRAME: if L_acc/λ₀ > 1000, use boost γ_b ≈ ω₀/ω_p.
   Check: NCI (numerical Cherenkov) mitigation method.

5. BOUNDARY CONDITIONS:
   - Laser injection: total-field/scattered-field (TFSF).
   - Particles: absorbing (leave domain), thermal re-injection.
   - Fields: PML (perfectly matched layer) for open boundaries.

6. OUTPUT: particle phase space (x,p_x,p_y,p_z), fields (E,B), current J.
   Diagnostics every ~10-100 timesteps (typical Δt ~ 0.1 fs for optical).
```

## Edge Cases

- **Numerical Cherenkov instability (NCI)**: in boosted-frame PIC, the
  grid dispersion supports spurious Cherenkov resonance with relativistic
  particles → exponential noise growth. Mitigation: FFT-based solvers
  (PSATD), low-pass filters, or moderate smoothing.
- **Statistical noise**: low particle-per-cell → noisy fields → artificial
  heating and diffusion. Merging/splitting particles in regions of extreme
  density change.
- **QED Monte Carlo statistics**: at χ_e ~ 1, multiple photons per timestep
  → sub-stepping or adaptive timestepping needed.

### Shape function noise and P3M (Hockney & Eastwood 2020, Ch.5,7-8)

The shape function S(x) determines both spatial resolution AND force noise:
```
⟨(δF)²⟩ ∝ (1/N_c) Σ_k |S(k)|² k² |φ(k)|²
```
where N_c is the number of superparticles per Debye sphere. Lower-order
shape functions (NGP) produce more high-k noise; higher-order (CIC, TSC)
suppress it at the cost of wider stencil:

| Shape | Order | Stencil width | Noise level | Force accuracy |
|-------|-------|--------------|-------------|---------------|
| **NGP** (nearest grid point) | 0 | 1 cell | High | O(Δx) |
| **CIC** (cloud-in-cell) | 1 | 2 cells | Medium | O(Δx²) |
| **TSC** (triangular shaped cloud) | 2 | 3 cells | Low | O(Δx³) |

**P3M (Particle-Particle Particle-Mesh)**: for problems where close encounters
matter (ν_coll not negligible), supplement the PM force with direct PP
corrections at r < r_cut. The short-range force is the EXACT Coulomb/gravitational
force minus the mesh-smoothed component to avoid double-counting. P3M
complexity is O(N_p N_nb + N_g log N_g), intermediate between PM and full PP.

**Universal collisionless condition** (Hockney §1-3): the model remains
collisionless when N_c ≫ 1 and timescales are short compared to the
numerical relaxation time τ_coll ≈ N_c T_p (λ_D/Δx)³. This condition
applies identically to plasma PIC, N-body galaxy simulations, and MD
— in all cases, the shape function S(x) smooths short-range forces
to suppress artificial two-body relaxation.

## Cross-References

- Birdsall & Langdon, *Plasma Physics via Computer Simulation* (2018)
- Macchi §9, Pukhov (2003) — Virtual Laser-Plasma Lab (VLPL)
- Arber et al., PPCF 2015 — EPOCH code
- computational-physics: reasoning.cp.fdtd_yee_algorithm (parent — Yee solver)
- computational-physics: reasoning.cp.moment_method (fluid vs kinetic comparison)
- laser-plasma: reasoning.lp.strong_field_qed_plasma (QED modules)
