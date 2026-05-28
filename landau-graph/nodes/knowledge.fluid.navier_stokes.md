---
skill_id: knowledge.fluid.navier_stokes
type: knowledge
summary_50t: >
  ρ(∂v/∂t+v·∇v) = −∇p + η∇²v + (ζ+η/3)∇(div v). Re = ul/ν.
  Incompressible: ∂v/∂t+v·∇v = −∇p/ρ + ν∇²v. Re determines regime.
trigger:
  - viscous fluid flow
  - friction, drag, dissipation in fluids
  - transition to turbulence
reasoning_role: viscous_fluid_dynamics
parent: reasoning.constitutive_relation_from_symmetry
children:
  - knowledge.fluid.reynolds_similarity
retrieval_cost: 1
---

# knowledge.fluid.navier_stokes

**Full**: ρ(∂v_i/∂t + v_k ∂v_i/∂x_k) = −∂p/∂x_i + ∂σ'_ik/∂x_k.
σ'_ik = η(∂v_i/∂x_k + ∂v_k/∂x_i − 2/3 δ_ik div v) + ζδ_ik div v.

**Incompressible** (∇·v=0): ∂v/∂t + (v·∇)v = −∇p/ρ + ν∇²v.
ν = η/ρ (kinematic viscosity). One parameter determines all viscous effects.

**Reynolds number**: Re = ul/ν. Ratio of inertial to viscous forces.
Re ≪ 1: Stokes flow (viscous dominated, linear, reversible).
Re ~ 1-10³: laminar flow. Re ≫ 10³: turbulence.

**Energy dissipation**: dE_kin/dt = −(η/2)∫(∂v_i/∂x_k + ∂v_k/∂x_i)² dV ≤ 0.
Viscosity always dissipates kinetic energy → heat.

**Exact solutions**: Poiseuille (pipe flow), Couette (rotating cylinders),
Stokes (creeping flow around sphere: drag F = 6πηaU).

- Landau Vol.6 §15-25
