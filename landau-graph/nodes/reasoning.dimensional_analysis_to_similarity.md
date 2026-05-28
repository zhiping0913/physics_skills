---
skill_id: reasoning.dimensional_analysis_to_similarity
type: reasoning
summary_50t: >
  Incompressible viscous flow has 3 parameters (ν,l,u) → 1 dimensionless
  number: Re = ul/ν. Flows with same Re and geometry are similar.
  This is Π-theorem applied to fluid dynamics.
trigger:
  - need to scale experimental results
  - determining flow regime (laminar vs turbulent)
  - similarity parameters for any physical system
reasoning_role: scaling_analysis
parent: reasoning.homogeneity_to_scaling
children:
  - knowledge.fluid.reynolds_similarity
retrieval_cost: 1
---

# reasoning.dimensional_analysis_to_similarity — Parameters → Dimensionless Numbers → Similarity

## Core Picture

Given a physical problem with n parameters expressed in k fundamental
dimensions, there are exactly n−k independent dimensionless combinations
(Π-theorem). For incompressible viscous flow: ν [L²/T], l [L], u [L/T]
→ 3−2 = 1 dimensionless number: Re = ul/ν.

ALL dimensionless quantities (velocity profiles, drag coefficients) are
functions of Re alone. Two flows with the same Re are similar.

## Algorithm

```
1. List all governing parameters (ν, l, u for incompressible viscous flow)
2. Determine their dimensions in [M,L,T]
3. Count independent dimensions → n−k dimensionless groups
4. Form the groups: Re = ul/ν
5. Write any physical quantity Q as: Q = [dimensionful combination] × f(Π₁, Π₂, ...)
```

## Beyond Reynolds

| Problem | Parameters | Dimensionless numbers |
|---------|-----------|----------------------|
| Compressible flow | +c (sound speed) | Re + M = u/c (Mach) |
| With gravity | +g | Re + Fr = u²/lg (Froude) |
| With surface tension | +α | Re + We = ρu²l/α (Weber) |
| Unsteady | +τ (timescale) | Re + St = uτ/l (Strouhal) |
| Heat transfer | +κ (thermal diffusivity) | Re + Pr = ν/κ (Prandtl) |

## Key Insight

Reynolds number measures the ratio of inertial to viscous forces:
Re = ρu²/(ηu/l) = inertial stress / viscous stress.
Re ≪ 1: viscous dominated (Stokes flow). Re ≫ 1: inertia dominated → turbulence.

## Cross-References
- Landau Vol.6 §19 (similarity law)
- Landau Vol.1 §10 (mechanical similarity — same idea, different context)
- Landau Vol.5 §53 (heat transfer similarity — Prandtl, Nusselt numbers)
