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
parent: reasoning.equilibrium_as_extremum
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
  OVERSpecification — no solution exists in general (Jackson §1.9).
- **Mixed BCs**: Dirichlet on part of ∂V, Neumann on another part also
  yields a unique solution. The proof still holds because U(∂U/∂n)=0 on
  each part separately.
- **Unbounded domains**: Φ→0 (or ∂Φ/∂n→0 sufficiently fast) at infinity
  replaces the finite ∂V condition.
- **Floating conductors**: Φ is constant but UNKNOWN on the surface. An
  additional constraint (e.g., total charge) determines it.
- **Sommerfeld radiation condition**: For exterior (unbounded) wave problems,
  the solution must represent OUTGOING waves at infinity:
  lim_{r→∞} r(∂U/∂r − ikU) = 0. This selects the physical solution
  among mathematically valid ones. Same pattern as `reasoning.physical_solution_selection`.
  (Jackson §9.1, §10.1; Chew §1)

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
