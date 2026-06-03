---
skill_id: reasoning.em.green_function_poisson
type: reasoning
summary_50t: >
  Solution to ∇²φ=−ρ/ε₀ with BCs is φ(r)=∫G(r,r')ρ(r')dV' + surface term.
  G(r,r') is the response to a point source at r' satisfying the SAME BCs.
  Method-of-images gives G for half-space; Legendre expansion for sphere.
trigger:
  - solving Poisson/Laplace with arbitrary sources and boundaries
  - need systematic method beyond guessing image charges
  - computing potential from known charge distribution
reasoning_role: poisson_green_function
parent: reasoning.retarded_green_function
retrieval_cost: 1
references:
  - landau-graph: reasoning.retarded_green_function (wave Green's function analog)
---

# reasoning.em.green_function_poisson — Point Source → Full Solution

## Core Picture

The Green's function G(r,r') for Poisson's equation is the potential at r
due to a UNIT point charge at r', satisfying the SAME boundary conditions
as the actual problem:

```
∇²G(r,r') = −δ(r−r')/ε₀    in V
G = 0 (Dirichlet) or ∂G/∂n = 0 (Neumann)    on ∂V
```

Once G is found, the solution for ANY source ρ is:

```
φ(r) = ∫_V G(r,r') ρ(r') dV' + ε₀ ∮_{∂V} [G ∂φ/∂n' − φ ∂G/∂n'] dS'
```

The surface integral vanishes if we use the proper Green's function type.

## Algorithm

```
1. Determine the Green's function for the geometry:
   Infinite space: G = 1/(4πε₀|r−r'|)  (the Coulomb kernel)
   Half-space (z>0, grounded plane): G = (1/4πε₀)(1/|r−r'| − 1/|r−r'_image|)
   Sphere (radius a, grounded): G expressed as Legendre series
   Cylindrical: G expressed as Bessel series

2. Method of images for G:
   For simple geometries, G = G_free + G_image where G_image accounts
   for boundary conditions. The image contribution has NO sources in V
   (∇²G_image = 0 in V).

3. Convolve with source: φ(r) = ∫ G(r,r') ρ(r') dV'.

4. For Laplace equation (ρ=0): solution is determined entirely by BCs
   → eigenfunction expansion (separation of variables).
```

## Key Examples

**Infinite space** (Jackson §1.10):
G(r,r') = 1/(4πε₀|r−r'|) → φ(r) = (1/4πε₀)∫ ρ(r')/|r−r'| dV'.
This is the Coulomb integral.

**Grounded conducting sphere, radius a** (Jackson §2.6):
Place image charge q' = −(a/r')q at r'' = (a²/r'²)r'. The Green's function
incorporates this automatically → solution for arbitrary ρ inside sphere.

**Cylindrical geometry** (Jackson §3.11):
G expressed as Fourier-Bessel integral: G = (1/2π)∫ e^{im(φ−φ')} ×
∫ J_m(kρ)J_m(kρ') e^{−k|z−z'|} dk.

## Connection to Retarded Green's Function

The Poisson Green's function is the STATIC limit of the retarded Green's
function: G_ret(r,t; r',t') = δ(t−t'−|r−r'|/c)/|r−r'| → δ/|r−r'| as c→∞.
The method-of-images construction for Poisson G generalizes to the
time-dependent case (images with time delays).

## Cross-References

- Jackson §1.10, §2.6, §3.11
- Griffiths §3.2-3.3
- landau-graph: reasoning.retarded_green_function (wave analog)
