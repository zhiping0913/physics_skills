---
skill_id: reasoning.dirac_equation_antiparticles
type: reasoning
summary_50t: >
  (iγ^μ∂_μ − m)ψ = 0. First-order relativistic wave equation.
  Spin emerges from rotational invariance. Negative-energy solutions
  → antiparticles (positrons). The Dirac sea picture.
trigger:
  - relativistic spin-½ particle dynamics
  - need to understand antiparticles
  - spin as relativistic necessity
reasoning_role: relativistic_quantum_theory
parent: reasoning.lorentz_invariance_to_action
children:
  - knowledge.qed.dirac_equation
retrieval_cost: 1
---

# reasoning.dirac_equation_antiparticles — Lorentz + Quantum → Dirac Equation → Antimatter

## Core Picture

The Klein-Gordon equation (□+m²)ψ = 0 is relativistic but second-order.
Dirac asked: can we get a first-order equation? The answer requires
4×4 matrices (γ^μ) and a 4-component wave function (bispinor).

The result: particles with spin-½ EMERGE from the marriage of quantum
mechanics and special relativity. Even more remarkably, the equation
has negative-energy solutions that Dirac brilliantly interpreted as
antiparticles — the positron, discovered 4 years later (1932).

## Algorithm (Dirac's Derivation)

```
1. Demand: (iγ^μ∂_μ − m)ψ = 0 must imply (□+m²)ψ = 0
2. This requires {γ^μ,γ^ν} = γ^μγ^ν + γ^νγ^μ = 2g^{μν}
3. Smallest matrices satisfying this: 4×4 (Dirac matrices)
4. Wave function ψ is a 4-component bispinor
5. Spin operator: S = (ℏ/2)Σ, Σ = diag(σ,σ)
   → spin-½ is BUILT IN, not added by hand
6. Free-particle solutions: ψ = u(p)e^{−ipx} (positive energy)
   and ψ = v(p)e^{+ipx} (negative energy)
7. Negative energy states reinterpreted as antiparticles:
   positron = hole in the Dirac sea
```

## Why Spin Emerges

In non-relativistic QM, spin is an ADDED degree of freedom.
In Dirac theory, spin is REQUIRED by Lorentz invariance — you cannot
have a first-order relativistic wave equation without it.

**Why four components (two spinors)**: A single 2-component Weyl spinor
can only give a massless wave equation. To introduce mass (a dimensionful
parameter), you MUST couple two spinors — ξ and η. Mass is the reason
the Dirac wave function has four components, not two.

**Parity invariance is automatic**: The two-spinor structure means the
wave equation is automatically invariant under spatial inversion
(P: ξ↔iη) — parity is not assumed, it FOLLOWS from the formalism.

## Antiparticles

Charge conjugation: ψ → ψ_c = C ψ̄^T. For Dirac: C = iγ²γ⁰.
Antiparticle has opposite charge, same mass. CPT theorem guarantees
particle ↔ antiparticle symmetry.

## Cross-References
- Landau Vol.4 §20-22 (Dirac equation), §25 (spin-statistics)
- Landau Vol.2 §8 (relativistic action) — classical foundation
- Landau Vol.3 §54-55 (Pauli equation, spin in non-relativistic QM)
