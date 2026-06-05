---
skill_id: mathematics.vector_green_identities
type: reasoning
summary_50t: >
  Green's identities: scalar ∮(φ∇ψ−ψ∇φ)·dS = ∫(φ∇²ψ−ψ∇²φ)dV.
  Vector: ∮[a×∇×b − b×∇×a + a(∇·b) − b(∇·a)]·dS = ... .
  Dyadic: ∮[∇×G̿·a − G̿·∇×a + (∇·G̿)a − G̿(∇·a)]·dS = ... .
  Stratton-Chu formula from vector Green's identity with Helmholtz fields.
trigger:
  - deriving integral representations from differential equations
  - constructing Huygens principle, equivalence theorem, boundary integral equations
reasoning_role: green_identities_hierarchy
parent: mathematics.dyadic_algebra
retrieval_cost: 1
---

# mathematics.vector_green_identities — Scalar → Vector → Dyadic

## Core Picture

Green's identities generalize integration by parts to multidimensional integrals.
Starting from the divergence theorem, three levels are built:
- **Scalar**: for Poisson/Helmholtz equations
- **Vector**: for Maxwell's equations (Stratton-Chu formula)
- **Dyadic**: for dyadic Green's function integral representations

The pattern at every level: `boundary surface integral = volume integral of
differential operators`. This is the mathematical foundation of the equivalence
principle, boundary integral equations, and Huygens' principle.

## Derivation Sketch

Starting from `mathematics-theorems: mathematics.dyadic_algebra` (products
between dyadics and vectors) and the divergence theorem:

### Level 1 — Scalar Green's Identities

Divergence theorem: ∫_V ∇·F dV = ∮_S F·n̂ dS.
Let F = φ∇ψ. Then ∇·(φ∇ψ) = ∇φ·∇ψ + φ∇²ψ:
```
∮_S φ ∂ψ/∂n dS = ∫_V (∇φ·∇ψ + φ∇²ψ) dV          [Green's 1st identity]
```
Swap φ↔ψ and subtract:
```
∮_S (φ ∂ψ/∂n − ψ ∂φ/∂n) dS = ∫_V (φ∇²ψ − ψ∇²φ) dV   [Green's 2nd identity]
```
This is the workhorse: from ∇²ψ = −ρ/ε₀ (Poisson), Green's 2nd identity gives
φ(r) = ∫_V G(r,r') ρ(r') dV' + boundary terms. The KEY stepping stone to
all integral equation methods.

### Level 2 — Vector Green's Identities (Stratton-Chu)

For vector fields satisfying Helmholtz (∇²+k²)E = 0, use the vector-dyadic
divergence theorem with a = E, b = G(r,r')c (G scalar, c constant vector):
```
∮_S [n̂×E·∇×G + (n̂×E)×∇G + (n̂·E)∇G] dS = ... (Stratton-Chu)
```
After eliminating the arbitrary constant vector c, the Stratton-Chu formula:
```
E(r) = ∮_S [iωμ₀ (n̂×H)G + (n̂×E)×∇G + (n̂·E)∇G] dS     for r ∈ V
     = 0                                                    for r ∉ V
```
This is the VECTOR generalization of the Helmholtz-Kirchhoff integral. It
exactly represents the field inside V in terms of tangential E, H on S.

### Level 3 — Dyadic Green's Identities

For dyadic G̿ satisfying ∇×∇×G̿ − k²G̿ = I̿ δ(r−r'):
```
∮_S [∇×G̿·a − G̿·∇×a + (∇·G̿)a − G̿(∇·a)]·n̂ dS = ...
```
The dyadic version provides the most compact formulation of the equivalence
principle for arbitrary vector sources.

## Algorithm — From Differential Equation to Integral Representation

```
1. Identify the differential operator L: Lu = f (Poisson, Helmholtz, Maxwell).
2. Find Green's function G satisfying LG = δ(r−r') (scalar) or L̿G̿ = I̿δ (dyadic).
3. Apply the appropriate level of Green's identity:
   Level 1 (scalar): for ∇²φ = −ρ/ε₀ → φ = ∫ Gρ dV' + surface term
   Level 2 (vector): for (∇²+k²)E = iωμ₀J → Stratton-Chu representation
   Level 3 (dyadic): for ∇×∇×E − k²E = iωμ₀J → E = iωμ₀∫ G̿_e·J dV' + ...
4. Evaluate surface integrals using the known BCs on S.
5. Specialize: Kirchhoff diffraction = scalar level with Kirchhoff BCs;
   equivalence principle = vector level with equivalent surface currents.
```

## Key Applications in Electrodynamics

| Green's Identity Level | EM Application |
|------------------------|---------------|
| Scalar 2nd identity | Kirchhoff diffraction integral, Poisson solver |
| Vector (Stratton-Chu) | Equivalence principle, aperture radiation |
| Dyadic | Method of Moments (EFIE/MFIE), dyadic Green's function construction |

## Edge Cases

- **Source on boundary**: The integral changes discontinuously by ½ when r→S.
  Solid-angle factor for non-smooth surfaces.
- **Multiply-connected domains**: Surface S must enclose V completely.
  Cut surfaces needed for toroidal geometries.
- **Radiation condition at infinity**: For exterior problems, the surface at
  infinity contributes zero ONLY when fields satisfy the Sommerfeld radiation
  condition (outgoing waves).

## Cross-References

- Tai, *General Vector and Dyadic Analysis* (1997) §4-9, §4-10, §7-2
- Stratton, *Electromagnetic Theory* (1941) §8.13-8.14
- mathematics-theorems: mathematics.dyadic_algebra (parent — dyadic product rules)
- electrodynamics: reasoning.em.uniqueness_theorem_boundary_value (uniqueness → well-posed integral formulation)
- electrodynamics: reasoning.em.green_function_poisson (scalar level application)
- electrodynamics: reasoning.em.dyadic_green_function (dyadic level application)
