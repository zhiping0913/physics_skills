---
skill_id: reasoning.continuum_limit_to_field_equations
type: reasoning
summary_50t: >
  Particle mechanics → continuum fields. Conservation laws become PDEs:
  ∂ρ/∂t + div(ρv) = 0, Euler eqn. This is the fundamental bridge from
  discrete to continuous descriptions of matter.
trigger:
  - deriving fluid equations from conservation laws
  - continuum modeling of any many-particle system
  - MHD, plasma fluid models, elasticity
reasoning_role: continuum_limit
parent: reasoning.ensemble_logic
children:
  - knowledge.fluid.euler_equation
  - knowledge.fluid.navier_stokes
retrieval_cost: 1
---

# reasoning.continuum_limit_to_field_equations — Particle Mechanics → Continuum PDEs

## Core Picture

**The continuum premise** (Landau §1): Every "infinitesimal" fluid element
is PHYSICALLY infinitesimal — small compared to the body (dV ≪ L³_body)
but large compared to molecular distances (dV ≫ a³_molecular), so it still
contains very many molecules. This scale separation justifies treating
density ρ(r,t), velocity v(r,t), and pressure p(r,t) as continuous fields.

**Eulerian description**: v(x,y,z,t) is the velocity AT a fixed point in
space at time t — NOT the velocity of a specific fluid particle. All
fields (ρ, p, v) are defined at spatial points. This choice of reference
frame is what makes the substantial derivative necessary.

**From conservation to PDEs**: Take the conservation laws of mechanics
(mass, momentum, energy) and apply them to the fluid continuum.

## Algorithm

**Mass (continuity):**
```
1. Mass in volume V₀: ∫ ρ dV
2. Flux through surface: ∮ ρv·df (outward normal)
3. Conservation: ∂/∂t ∫ ρ dV = −∮ ρv·df
4. Gauss theorem → ∂ρ/∂t + div(ρv) = 0
   ρ⁻¹ dρ/dt = −div v  (Lagrangian form)
```

**Momentum (Euler, then momentum flux):**
```
1. Force on fluid element: −∮ p df = −∫ ∇p dV → force per unit volume = −∇p
2. Acceleration = dV/dt = ∂v/∂t + (v·∇)v
3. Euler equation: ρ(∂v/∂t + v·∇v) = −∇p + f_ext
4. Momentum flux form (§7): ∂(ρv_i)/∂t = −∂Π_ik/∂x_k
   Π_ik = p δ_ik + ρ v_i v_k  (ideal fluid momentum flux tensor)
   → ∫ρv_i dV changes by flux of Π_ik through boundary
```
This momentum flux form is the bridge to Navier-Stokes (§15): viscous
fluid is obtained by adding σ'_ik to Π_ik.

**Adiabatic condition** (§2, four forms):
```
1. ds/dt = 0  (entropy conserved following a fluid particle)
2. ∂s/∂t + v·grad s = 0  (Eulerian form)
3. ∂(ρs)/∂t + div(ρsv) = 0  ("continuity equation for entropy")
4. s = const  (isentropic — special case: s initially uniform everywhere)
```
Only in the isentropic case can ∇p/ρ be written as ∇w where w = enthalpy.
This gives the alternative form: ∂v/∂t + (v·∇)v = −∇w.

**Closure**: p = p(ρ,s) from equation of state.

## The Substantial Derivative

d/dt = ∂/∂t + v·∇. This is NOT the change at a fixed point, but the
change following a fluid element. This non-linear term is the source
of all fluid dynamical complexity — it makes the equations capable of
describing turbulence, shocks, and vortices.

## Connection to Statistical Physics (Vol.5, 10)

The fluid equations are the MOMENT EQUATIONS of the Boltzmann equation.
The Euler equations are the zeroth-order truncation (local equilibrium).
The Navier-Stokes equations add the first-order correction (viscous stress
from non-equilibrium gradients).

## Cross-References
- Landau Vol.6 §1-2 (continuity, Euler)
- Landau Vol.5 → Vol.10: Boltzmann → moment hierarchy → fluid closure
- Landau Vol.8 §65: MHD = fluid + Maxwell
