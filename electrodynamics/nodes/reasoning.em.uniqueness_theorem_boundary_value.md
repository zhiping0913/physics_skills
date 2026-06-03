---
skill_id: reasoning.em.uniqueness_theorem_boundary_value
type: reasoning
summary_50t: >
  Given sources ρ,J in V and E×n or φ on ∂V, the solution to Maxwell
  is unique. This single theorem justifies ALL boundary-value methods
  (images, separation of variables, Green's functions) — if you find
  ANY solution meeting BCs, it is THE solution.
trigger:
  - solving EM problem with boundaries
  - need to justify method of images, eigenfunction expansion, or Green's function
  - verifying that a candidate solution is correct
reasoning_role: uniqueness_boundary_value
parent: landau-graph:reasoning.equilibrium_as_extremum
sign_convention: SI; Dirichlet (φ specified) and Neumann (∂φ/∂n specified) BC taxonomy
retrieval_cost: 1
references:
  - landau-graph: reasoning.equilibrium_as_extremum (analogy: unique extremum)
---

# reasoning.em.uniqueness_theorem_boundary_value — Boundary Conditions → Unique Solution

## Core Picture

For Poisson's equation ∇²φ = −ρ/ε₀ in a volume V:

**Theorem**: If φ is specified on ∂V (Dirichlet) OR ∂φ/∂n is specified on ∂V
(Neumann), the solution is UNIQUE (up to an additive constant for Neumann).

The proof is one line: suppose two solutions φ₁, φ₂ exist. Their difference
U = φ₁−φ₂ satisfies ∇²U = 0 in V and U=0 (or ∂U/∂n=0) on ∂V. Green's first
identity ∫(U∇²U + |∇U|²)dV = ∮U(∂U/∂n)dS → ∫|∇U|²dV = 0 → ∇U=0 → U=const.
For Dirichlet, U=0 on ∂V → U≡0. QED.

## Derivation Sketch

Starting from `landau-graph: reasoning.equilibrium_as_extremum` we have the
variational principle: δF = 0 with constraints gives the unique equilibrium
state. For electrostatics, F[φ] = ∫(½ε₀|∇φ|² − ρφ)dV is the energy functional;
its Euler-Lagrange equation δF/δφ = 0 → −ε₀∇²φ − ρ = 0 → ∇²φ = −ρ/ε₀. The
variational principle guarantees existence; uniqueness requires convexity:
F is strictly convex in φ, so the stationary point is the unique global minimum.

**Key non-obvious step — boundary conditions via Green's identity**: The
uniqueness proof uses Green's first identity, which is a disguised integration
by parts. The boundary term ∮U(∂U/∂n)dS vanishes for EITHER Dirichlet (U=0 on
∂V) OR Neumann (∂U/∂n=0 on ∂V), but NOT for both — specifying BOTH is the
ill-posed Cauchy problem. The identity ∫|∇U|²dV = 0 forces ∇U = 0 everywhere,
meaning the two candidate solutions differ by at most a constant.

**Stratton-Chu / Franz integral representation** (for vector Helmholtz): For
Maxwell's equations in source-free region, specifying n×E on ∂V gives a unique
solution via the vector Green's theorem (Stratton §8.14; Chew §1). This is the
full-wave generalization: the Stratton-Chu formula expresses E(r) inside V from
n×E and n×H on ∂V — but uniqueness requires only ONE of these (plus the
Sommerfeld radiation condition for unbounded domains; see Edge Cases).

## Why This Matters

This theorem is the central justification for ALL boundary-value techniques:

- **Method of images**: Don't solve the full PDE — guess an equivalent charge
  configuration outside V that produces the right BCs. If you find ANY
  configuration that works, uniqueness guarantees it's the right one.
- **Separation of variables**: The eigenfunction expansion gives ONE solution.
  Uniqueness guarantees you don't need to check for others.
- **Green's functions**: The Green's function construction produces a solution.
  Uniqueness guarantees it's the only one.

## Algorithm

```
1. Specify: PDE in V (∇²φ = −ρ/ε₀ or Helmholtz or wave equation).
2. Specify: Boundary conditions on ∂V (Dirichlet, Neumann, or mixed).
3. Find ANY solution that satisfies both.
4. Uniqueness theorem: that solution IS the unique physical answer.
5. Therefore: any SOLUTION METHOD (images, series, integral) is valid
   as long as it produces a solution meeting the BCs.
```

## Edge Cases

- **Cauchy BCs are INVALID**: Specifying BOTH Φ and ∂Φ/∂n on ∂V is an
  OVERSpecification — no solution exists in general (Jackson §1.9). When
  you think you need both, reformulate as a Dirichlet problem using the
  known surface charge density to fix φ, or as a Neumann problem using
  the known total charge on a conductor.
- **Mixed BCs**: Dirichlet on part of ∂V, Neumann on another part also
  yields a unique solution. The proof still holds because U(∂U/∂n)=0 on
  each part separately.
- **Unbounded domains — Sommerfeld radiation condition (the standard gap)**:
  For exterior (unbounded) wave problems, ∇²φ + k²φ = 0 has two mathematical
  solutions at infinity: incoming and outgoing waves. The Sommerfeld radiation
  condition lim_{r→∞} r(∂U/∂r − ikU) = 0 selects the physical OUTGOING wave.
  When this breaks down (e.g., in waveguides with multiple propagation
  directions), use the limiting-absorption principle (k→k+iε) or the
  Stratton-Chu integral representation to pick the causal solution.
  (Jackson §9.1, §10.1; Chew §1.)
- **Floating conductors**: Φ is constant but UNKNOWN on the surface. An
  additional constraint (e.g., total charge) determines it — use the
  method of undetermined constants: solve with Φ_c as a parameter, then
  impose ∫(∂φ/∂n)dS = −Q/ε₀.

## Extension to Maxwell's Equations

For time-harmonic fields in a source-free region, specifying n×E or n×H
on ∂V gives a unique solution to the vector Helmholtz equation. This is
the foundation for waveguide and cavity mode analysis.

## Connection to Variational Principle

This is the boundary-value analog of `reasoning.equilibrium_as_extremum`:
just as δF=0 with constraints gives the unique equilibrium state,
boundary conditions + PDE give the unique field configuration. Both
are instances of "constraints + governing equation → unique solution."

## Cross-References

- Jackson §1.9, §2.1 (uniqueness theorem, method of images justification)
- Griffiths §3.1.5-3.1.6 (uniqueness theorems)
- landau-graph: reasoning.equilibrium_as_extremum (analogy)
