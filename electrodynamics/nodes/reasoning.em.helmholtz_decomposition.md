---
skill_id: reasoning.em.helmholtz_decomposition
type: reasoning
summary_50t: >
  Any vector field F = −∇φ + ∇×A (scalar + vector potential). Imposed
  by div and curl: φ from ∇·F, A from ∇×F with ∇·A=0 gauge. This unlocks
  separation of electrostatics (∇×E=0 → E=−∇φ) from magnetostatics (∇·B=0 → B=∇×A).
trigger:
  - need to decompose a vector field into irrotational + solenoidal parts
  - solving Poisson/Laplace with sources
  - introducing potentials in EM
reasoning_role: vector_field_decomposition
parent: reasoning.gauge_invariance_to_field_tensor
retrieval_cost: 1
references:
  - landau-graph: reasoning.gauge_invariance_to_field_tensor
---

# reasoning.em.helmholtz_decomposition — Vector Field → Scalar + Vector Potential

## Core Picture

The Helmholtz theorem (fundamental theorem of vector calculus): any
sufficiently smooth vector field F(r) that vanishes at infinity can be
UNIQUELY decomposed as:

```
F = −∇φ + ∇×A
```

where φ(r) is the scalar potential (irrotational part, ∇×(−∇φ) = 0) and
A(r) is the vector potential (solenoidal part, ∇·(∇×A) = 0).

This is the mathematical foundation for the entire potential formulation
of electrodynamics. In 4D language, it generalizes to A^μ = (φ, A).

## Algorithm

```
1. Given F(r) with known ∇·F = s(r) and ∇×F = c(r).
2. Scalar potential: ∇²φ = −s(r) → φ(r) = ∫ s(r')/(4π|r−r'|) dV'.
3. Vector potential: ∇²A = −c(r) with gauge ∇·A = 0.
   → A(r) = ∫ c(r')/(4π|r−r'|) dV'.
4. Uniqueness requires boundary conditions (F→0 at ∞ for infinite space).
```

## Application to Electrodynamics

**Electrostatics** (∇×E = 0, ∇·E = ρ/ε₀):
→ E = −∇φ, ∇²φ = −ρ/ε₀. The curl-free condition means E is purely irrotational.

**Magnetostatics** (∇·B = 0, ∇×B = μ₀J):
→ B = ∇×A, ∇²A = −μ₀J (with ∇·A = 0). The divergence-free condition
means B is purely solenoidal.

**General time-dependent**: Both parts are needed. The 4-potential
A^μ = (φ/c, A) captures both simultaneously → gauge invariance.

## Connection to Gauge Freedom

The decomposition A is NOT unique: A → A + ∇χ leaves ∇×A unchanged.
This is the 3D origin of gauge invariance. The Coulomb gauge ∇·A = 0
is a natural choice from the Helmholtz decomposition perspective.

## Edge Cases

- **Uniqueness requires falloff faster than 1/r**: The decomposition is unique
  only if |F| → 0 faster than 1/r as r → ∞. A field falling as exactly 1/r
  admits multiple valid decompositions. Jackson §1.5 explicitly notes this
  fine print — it rarely matters practically but is the mathematical basis.
- **Multiply connected domains** (e.g., toroidal volumes): Additional harmonic
  components from cohomology are needed.
- **Non-vanishing at infinity** (uniform background field): The decomposition
  must include the background component explicitly.

## Cross-References

- Jackson §1.5-1.6 (Helmholtz theorem, potentials)
- Griffiths §1.6 (Helmholtz theorem)
- landau-graph: reasoning.gauge_invariance_to_field_tensor (4D generalization)
