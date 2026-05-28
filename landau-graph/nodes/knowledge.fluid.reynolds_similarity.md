---
skill_id: knowledge.fluid.reynolds_similarity
type: knowledge
summary_50t: >
  Re = ul/ν. Flows with same Re and geometry are similar.
  Drag coefficient C_D = C_D(Re). Low Re: C_D ∝ 1/Re (Stokes).
  High Re: turbulent boundary layer, crisis at Re ~ 10⁵.
trigger:
  - scaling flow experiments
  - determining drag, lift coefficients
  - estimating flow regime
reasoning_role: similarity_scaling
parent: reasoning.dimensional_analysis_to_similarity
retrieval_cost: 1
---

# knowledge.fluid.reynolds_similarity

**Reynolds number**: Re = ul/ν. Only dimensionless parameter for
incompressible viscous flow with fixed geometry.

**Similarity principle**: v/u = f(r/l, Re). p/(ρu²) = g(r/l, Re).
C_D = F/(½ρu²A) = C_D(Re) — drag coefficient depends ONLY on Re.

**Low Re (Stokes)**: Inertia neglected. Drag F ∝ ηul. C_D ∝ 1/Re.

**Intermediate Re**: Laminar boundary layer. C_D ~ const (form drag).

**High Re**: Turbulence. C_D approximately constant.
Drag crisis at Re ~ 10⁵ (sphere): laminar→turbulent transition in
boundary layer → separation delayed → C_D drops sharply.

**Additional dimensionless numbers** (when more physics added):
```
Mach     M = u/c        compressibility
Froude   Fr = u²/lg     gravity waves  
Weber    We = ρu²l/α   surface tension
Prandtl  Pr = ν/κ       heat transfer
Strouhal St = uτ/l      unsteadiness
```

- Landau Vol.6 §19, §45-47
