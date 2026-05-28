---
skill_id: reasoning.kinetic_equation_closure
type: reasoning
summary_50t: >
  ∂f/∂t + v·∇f + F·∂f/∂p = St f. The Boltzmann equation closes the hierarchy:
  binary collisions → collision integral. Without collisions: Vlasov equation.
  H-theorem: dH/dt ≤ 0 → approach to equilibrium.
trigger:
  - non-equilibrium gas or plasma
  - need evolution of distribution function
  - transport coefficients from microscopic dynamics
reasoning_role: kinetic_closure
parent: reasoning.ensemble_logic
children:
  - knowledge.kinetic.boltzmann_equation
  - knowledge.kinetic.landau_collision_integral
  - knowledge.kinetic.plasma_dielectric
retrieval_cost: 1
---

# reasoning.kinetic_equation_closure — Distribution Function → Kinetic Equation

## Core Picture

The distribution function f(t,r,p) gives the number of particles in d³r d³p.
Its evolution: ∂f/∂t + v·∇f + F·∂f/∂p = St f.

The left side is the Vlasov (collisionless) evolution.
The right side St f is the collision integral — it encodes how binary
collisions redistribute particles in momentum space.

This is the fundamental equation of non-equilibrium statistical physics.
Equilibrium is recovered as the stationary solution where St f = 0.

## Algorithm (Boltzmann)

```
1. Write streaming terms: particles move along trajectories between collisions
2. Collision term: for binary collisions a+b ↔ a'+b', 
   St f = ∫ w(p,p₁→p',p₁')[f'f₁' − ff₁] d³p₁ d³p' d³p₁'
   where w is the scattering probability (from cross-section)
3. H-theorem: H = ∫ f ln f d³p, dH/dt ≤ 0 (entropy increases)
4. Equilibrium: St f = 0 → f ∝ exp(−E/T) (Maxwell-Boltzmann)
5. Near equilibrium: Chapman-Enskog expansion → transport coefficients
```

## Collisionless Limit (Vlasov)

When collisions are negligible (high temperature, low density plasma):
∂f/∂t + v·∇f + F·∂f/∂p = 0, with F determined self-consistently:
F = q(E + v×B/c), div E = 4πρ, etc.

This is the starting point for Landau damping and plasma wave theory.

## Cross-References
- Landau Vol.10 §3 (Boltzmann equation), §29-30 (Landau damping)
- Landau Vol.5 §28 (equilibrium Gibbs distribution as stationary solution)
- Landau Vol.1 §46 (Liouville theorem)
