---
skill_id: knowledge.kinetic.vlasov_equation
type: knowledge
summary_50t: >
  ∂f/∂t + v·∇f + (q/m)(E + v×B/c)·∇_v f = 0. Collisionless Boltzmann
  equation for plasma. Self-consistent with Maxwell: ρ = q∫f d³v,
  j = q∫vf d³v. Foundation for Landau damping and plasma waves.
trigger:
  - collisionless plasma dynamics
  - deriving plasma dielectric function
  - kinetic instabilities
reasoning_role: kinetic_plasma
parent: reasoning.kinetic_equation_closure
retrieval_cost: 1
---

# knowledge.kinetic.vlasov_equation

**Vlasov equation** (collisionless Boltzmann equation for plasma):

∂f_α/∂t + v·∇f_α + (q_α/m_α)(E + v×B/c)·∇_v f_α = 0

where f_α(r,v,t) is the distribution function for species α.

**Self-consistent fields** (Maxwell equations with plasma sources):
ρ = Σ q_α ∫ f_α d³v,   j = Σ q_α ∫ v f_α d³v

**Key properties**:
- Time-reversible (unlike Boltzmann with collisions)
- Nonlinear: v·∇_v couples different velocity moments
- Coupled to Maxwell: fields depend on f, f depends on fields

**Linearized Vlasov** (for small perturbations δf around equilibrium f₀):
∂δf/∂t + v·∇δf + (q/m)E₁·∇_v f₀ = 0  (B₀ term dropped for unmagnetized)

**Landau's solution** (Vol.10 §29-30):
- Laplace transform in time, Fourier in space
- δf_k(v,ω) = −i(q/m)E_k·∇_v f₀ / (ω − k·v)
- Integration over v → plasma dielectric ε_l(k,ω)
- Pole at ω = k·v → Landau damping from analytic continuation

**Critical subtlety** (Vol.10 rumination): The order of limits matters.
Linearize FIRST, then take collisionless limit ν→0. Reversed order
produces a singularity at the resonance. See `reasoning.physical_solution_selection`.

- Landau Vol.10 §27-30 (Vlasov, plasma dielectric, Landau damping)
