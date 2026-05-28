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

## Kolmogorov Turbulence: Dimensional Analysis at Its Peak

The Richardson-Kolmogorov theory of developed turbulence (§33) is arguably
the most impressive application of dimensional analysis in physics.
The reasoning uses ONLY ε (energy dissipation per unit mass) and λ (scale),
with NO free parameters:

```
v_λ ∼ (ε·λ)^{1/3}                     (Kolmogorov-Obukhov law, 33.6)
E(k) ∼ ε^{2/3}·k^{-5/3}              (energy spectrum in inertial range)
λ₀ ∼ (ν³/ε)^{1/4}                     (Kolmogorov dissipation scale, 33.10)
ε ∼ (Δu)³/l                           (dissipation from large scales, 33.1)
```

**The reasoning** (§33):
1. For scales λ ≫ λ₀, viscosity ν is irrelevant → v_λ can only depend on ε and λ.
2. [ε] = cm²/s³, [λ] = cm → unique combination with [v] = cm/s is (ελ)^{1/3}.
3. The energy cascades from large to small scales without dissipation
   (Richardson cascade). Dissipation only occurs at λ ∼ λ₀.
4. The k^{-5/3} spectrum follows from Fourier transform of (33.6).

**This is dimensional analysis in its purest form**: two quantities
(ε, λ) → one unique velocity scale. No PDE solving, no free parameters.
The only "input" is the physical insight that ν is irrelevant for λ ≫ λ₀.

**Cross-References**

- Landau Vol.6 §19 (similarity law), §33 (developed turbulence)
- reasoning.homogeneity_to_scaling (Vol.1) — same logic applied to mechanics
