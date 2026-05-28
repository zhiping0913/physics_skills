---
skill_id: knowledge.fluid.euler_equation
type: knowledge
summary_50t: >
  ∂v/∂t + v·∇v = −∇p/ρ. Ideal fluid. Circulation ∮v·dl conserved (Kelvin).
  Vorticity frozen into fluid. Bernoulli: v²/2 + w + gz = const along streamline.
trigger:
  - ideal (inviscid) fluid flow
  - vortex dynamics
  - Bernoulli principle
reasoning_role: ideal_fluid_dynamics
parent: reasoning.continuum_limit_to_field_equations
retrieval_cost: 1
---

# knowledge.fluid.euler_equation

**Euler equation**: ∂v/∂t + (v·∇)v = −(1/ρ)∇p + g.
With continuity: ∂ρ/∂t + div(ρv) = 0.

**Kelvin circulation theorem** (§8): d/dt ∮v·dl = 0 for ideal barotropic fluid.
Vorticity ω = rot v is "frozen in" — vortex lines move with the fluid.

**Bernoulli**: For steady, ideal, incompressible flow:
v²/2 + p/ρ + gz = const along a streamline.
For compressible isentropic: v²/2 + w + gz = const (w = enthalpy).

**Potential flow**: If ω = 0 everywhere, v = ∇φ, and ∇²φ = 0 (Laplace eqn).
d'Alembert's paradox: potential flow past a body produces ZERO drag.

**Limitations**: No dissipation, no vorticity generation, no turbulence.
Real fluids require viscosity (Navier-Stokes).

- Landau Vol.6 §1-14
