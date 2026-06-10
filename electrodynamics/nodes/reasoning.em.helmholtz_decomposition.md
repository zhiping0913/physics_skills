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
parent: landau-graph:reasoning.gauge_invariance_to_field_tensor
sign_convention: SI; E=−∇φ (minus sign convention for scalar potential)
retrieval_cost: 1
references:
  - landau-graph: reasoning.gauge_invariance_to_field_tensor
---

# reasoning.em.helmholtz_decomposition — Vector Field → Scalar + Vector Potential

## Core Picture

The Helmholtz theorem (fundamental theorem of vector calculus): any
sufficiently smooth vector field F(r) that vanishes at infinity can be
UNIQUELY decomposed as (for lossless isotropic media). In anisotropic and
viscoelastic media (Wave Fields in Real Media 2022, Ch.4): the Lamé constants
become complex, frequency-dependent tensors C_{ijkl}(ω), the P/S wave
decoupling is generally lost, and the Helmholtz decomposition is replaced by
the Christoffel equation det(C_{ijkl} n_j n_l − ρv² δ_{ik}) = 0. This connects to
`plasma.dielectric_tensor_magnetized` (anisotropic ε_{ik}) and
`em.nonlinear_optical_response` (frequency-dependent χ^{(n)}).

```
F = −∇φ + ∇×A
```

where φ(r) is the scalar potential (irrotational part, ∇×(−∇φ) = 0) and
A(r) is the vector potential (solenoidal part, ∇·(∇×A) = 0).

This is the mathematical foundation for the entire potential formulation
of electrodynamics. In 4D language, it generalizes to A^μ = (φ, A).

## Derivation Sketch

Starting from `landau-graph: reasoning.gauge_invariance_to_field_tensor` we have
the 4-potential A^μ = (φ/c, A) unifying scalar and vector potentials under gauge
transformations A^μ → A^μ + ∂^μχ. The 3D projection of this structure IS the
Helmholtz decomposition: the time component gives the irrotational part (−∇φ),
the spatial components give the solenoidal part (∇×A).

**Key non-obvious step — Coulomb gauge as the natural split**: The gauge freedom
A → A + ∇χ means the decomposition is NOT unique a priori. Imposing the Coulomb
gauge ∇·A = 0 removes the ambiguity: it projects out the longitudinal (irrotational)
component of A, leaving only the transverse (solenoidal) degrees of freedom.
In Fourier space this is the transverse projection operator:

```
P_⊥ = 1 − k̂k̂    →    A_⊥(k) = P_⊥·A(k) satisfies k·A_⊥ = 0
```

The Coulomb gauge cleanly separates the instantaneous Coulomb interaction
(irrotational, longitudinal E_L = −∇φ with ∇·E_L = ρ/ε₀) from the radiative
degrees of freedom (solenoidal, transverse E_T = −∂A/∂t with ∇·E_T = 0).
This split is essential for quantization: only the transverse part of A
corresponds to physical photons; the longitudinal part is a constrained
degree of freedom eliminated by Gauss's law.

**Multiply-connected domains**: In toroidal volumes (genus ≥ 1), additional
harmonic components from de Rham cohomology appear — vector fields with both
∇·F = 0 and ∇×F = 0 that are NOT gradients of single-valued potentials.
These require Hodge decomposition with harmonic forms (Jackson §1.5).

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
  admits multiple valid decompositions. When this occurs, use the explicit
  Coulomb-kernel construction φ = ∫(∇·F)/4π|r−r'|dV' + surface terms to fix a
  unique decomposition (Jackson §1.5).
- **Multiply-connected domains** (e.g., toroidal volumes): Helmholtz alone is
  insufficient — switch to Hodge decomposition including harmonic forms to
  capture cohomology components (e.g., a DC magnetic flux threading a torus
  has B = ∇×A locally but ∮A·dl ≠ 0 globally).
- **Non-vanishing at infinity** (uniform background field): The decomposition
  must include the background component explicitly: F = F_bg + (−∇φ + ∇×A),
  where F_bg is the uniform background field.

## Cross-References

- Jackson §1.5-1.6 (Helmholtz theorem, potentials)
- Griffiths §1.6 (Helmholtz theorem)
- landau-graph: reasoning.gauge_invariance_to_field_tensor (4D generalization)
