---
skill_id: reasoning.canonical_transformation
type: reasoning
summary_50t: >
  The Hamiltonian formalism permits a vast class of coordinate-impulse
  transformations that preserve the canonical equations. The generating
  function F(q,Q,t) encodes the entire transformation.
trigger:
  - switching between equivalent Hamiltonian descriptions
  - simplifying H by clever variable choice
  - constructing action-angle variables
reasoning_role: generating_function_logic
parent: reasoning.variational_principle
children:
  - knowledge.mechanics.hamilton_equations
  - knowledge.mechanics.poisson_brackets
  - knowledge.mechanics.action_angle_variables
related:
  - reasoning.separation_of_variables
  - reasoning.adiabatic_invariance
retrieval_cost: 1
---

# reasoning.canonical_transformation — Generating Function → Equivalent Description

## Core Picture

Lagrange equations are invariant under point transformations q → Q(q,t).
Hamilton equations admit a MUCH larger class: any transformation
(p,q) → (P,Q) that preserves the form of the canonical equations.

The condition: Σ pᵢ dqᵢ − H dt = Σ Pᵢ dQᵢ − H' dt + dF.

F is the generating function. Its choice defines the transformation.
This freedom is the Hamilton formalism's greatest power.

## Algorithm

```
1. Choose a generating function in one of four forms:
   F₁(q,Q,t): p = ∂F₁/∂q,  P = −∂F₁/∂Q
   F₂(q,P,t): p = ∂F₂/∂q,  Q = ∂F₂/∂P   (most common)
   F₃(p,Q,t): q = −∂F₃/∂p, P = −∂F₃/∂Q
   F₄(p,P,t): q = −∂F₄/∂p, Q = ∂F₄/∂P
2. New Hamiltonian: H' = H + ∂F/∂t
3. If F doesn't depend explicitly on time: H' = H.
   Just express H in new variables.
4. Poisson brackets are INVARIANT under canonical transformations:
   {f,g}_{p,q} = {f,g}_{P,Q}
```

## The Point Transformation as Special Case

F₂ = Σ fᵢ(q,t) Pᵢ → Qᵢ = fᵢ(q,t). This is the Lagrangian-level
point transformation, now seen as a special case of the much broader
canonical class.

## Physical Meaning dissolves

After a general canonical transformation, Q is NOT a "position" and P
is NOT a "momentum" in the original sense. They are canonically conjugate
variables, period. The transformation Q = p, P = −q is perfectly valid —
it just swaps coordinate and momentum.

## Edge Cases

- **Time-dependent F**: H' ≠ H. The new Hamiltonian is not the energy.
- **Non-canonical transformations**: Do not preserve the symplectic structure.
  Poisson bracket invariance is THE test.

## Legendre Transform: A Cross-Volume Universal

The transformation L(q,q̇) → H(p,q) via H = Σ pᵢq̇ᵢ − L is the Legendre
transform. This is NOT just a mechanics trick — it is a universal
mathematical pattern appearing across ALL of theoretical physics:

| Domain | Original function | Transformed function | Relation |
|--------|------------------|---------------------|----------|
| Mechanics (V1) | L(q,q̇) | H(p,q) | H = Σ pᵢq̇ᵢ − L |
| Thermodynamics (V5) | E(S,V,N) | F(T,V,N) | F = E − TS |
| Thermodynamics (V5) | F(T,V,N) | Ω(T,V,μ) | Ω = F − μN |
| Elasticity (V7) | F(u_ik) | σ_ik(u) | σ_ik = ∂F/∂u_ik |
| Dielectrics (V8) | F(E) | F̃(D) | F̃ = F − E·D/4π |
| QFT (V4) | L(φ,∂φ) | H(π,φ) | H = πφ̇ − L |

The MATHEMATICS is identical in all cases: given F(x) (convex),
define G(y) = F(x) − xy where y = dF/dx. Then dG/dy = −x.
This is the mechanism behind:
- Canonical transformations (generating functions)
- Thermodynamic potentials (all four: E, F, H, G)
- Effective action in QFT (1PI generating functional)

**Key insight for agents**: When you encounter a new type of "energy" or
"potential" in ANY volume, ask: is this a Legendre transform of a more
fundamental function? The answer is almost always yes.

## Cross-References

- Landau Vol.1 §45 (Canonical transformations), §46 (Liouville theorem)
- The motion itself (t → t+τ) is a canonical transformation with F = action
- Quantum: unitary transformations are the operator analog
