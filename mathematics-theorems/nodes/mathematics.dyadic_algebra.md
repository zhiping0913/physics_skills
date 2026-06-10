---
skill_id: mathematics.dyadic_algebra
type: knowledge
summary_50t: >
  Dyadic D̿ = Σ_{i,j} D_{ij} x̂_i x̂_j. Nine components, transforms as
  D'_{mn} = Σ a_{mi} a_{nj} D_{ij}. Products: dot (D̿·F vector), cross
  (D̿×F dyadic), double-dot (D̿:G̿ scalar). Symmetric/antisymmetric/unit
  dyadic I̿ = Σ x̂_i x̂_i. Inverse D̿⁻¹. Eigen dyadics λ_i û_i û_i.
trigger:
  - need dyadic/tensor algebra for EM field problems
  - Green's dyadic, susceptibility tensor, stress dyadic operations
reasoning_role: dyadic_algebra
parent: mathematics.vector_algebra
retrieval_cost: 1
---

# mathematics.dyadic_algebra — Vector Pairs → 9-Component Dyadics

## Core Picture

A dyadic D̿ is formed by juxtaposing three vector functions with three unit
vectors: D̿ = Σ_j F_j x̂_j. In Cartesian coordinates this yields nine dyadic
components D_{ij} x̂_i x̂_j. The dyadic is the natural representation for
linear operators mapping vectors to vectors in 3D Euclidean space — the
mathematical foundation of Green's dyadics, susceptibility tensors, and
stress tensors in electrodynamics.

## Derivation Sketch

From `mathematics-theorems: mathematics.vector_algebra` (a vector F = Σ F_i x̂_i):

1. **Construction**: Take three independent vector functions F_j (j=1,2,3),
   each with three scalar components F_{ij}. Juxtapose with unit vectors:
   ```
   D̿ = Σ_{j} F_j x̂_j = Σ_{i,j} D_{ij} x̂_i x̂_j
   ```
   The pair x̂_i x̂_j is called a DYAD. D_{ij} are the nine scalar components.
   Under coordinate rotation x̂'_m = Σ a_{mi} x̂_i:
   ```
   D'_{mn} = Σ_{i,j} a_{mi} a_{nj} D_{ij}
   ```
   This is the transformation rule of a rank-2 tensor. A dyadic written in
   rectangular coordinates is called a Cartesian dyadic.

2. **Key distinction**: A dyad x̂_i x̂_j is ordered — x̂_i x̂_j ≠ x̂_j x̂_i.
   The transpose D̿^T has components (D̿^T)_{ij} = D_{ji}.

3. **Constructive pattern — when to reach for dyadics**:
   ```
   Given: a physical problem involving a LINEAR MAP F → G in 3D
   Step 1: Identify the input vector (e.g., current J, field E, strain)
           and the output vector (e.g., field E, displacement D, stress)
   Step 2: Represent the linear operator as a dyadic D̿ such that G = D̿·F.
           Build D̿ from symmetry, boundary conditions, or constitutive law.
   Step 3: Select the appropriate product from the Operations catalog:
           dot (·) for vector output, double-dot (:) for scalar invariants,
           cross (×) for rotation-like maps.
   Step 4: Exploit classification — if D̿ is symmetric, diagonalize via
           eigen-dyadic; if antisymmetric, reduce to vector a via A̿ = I̿ × a.
   ```

## Operations — Product Catalog

```
1. DOT PRODUCT (dyadic · vector → vector):
   D̿ · F = Σ_{i,j,k} D_{ij} (x̂_i x̂_j) · (F_k x̂_k)
          = Σ_{i,j} D_{ij} F_j x̂_i
   Vector · dyadic: F · D̿ = Σ_{i,j} F_i D_{ij} x̂_j
   Result is a VECTOR. In matrix form: (D̿·F)_i = Σ_j D_{ij} F_j.

2. CROSS PRODUCT (dyadic × vector → dyadic):
   D̿ × F = Σ_{i,j,k} D_{ij} (x̂_i x̂_j) × (F_k x̂_k)
          = Σ_{i,j,k} D_{ij} F_k ε_{jkm} x̂_i x̂_m
   Result is a DYADIC.

3. DOUBLE-DOT PRODUCT (dyadic : dyadic → scalar):
   D̿ : G̿ = Σ_{i,j} D_{ij} G_{ji}
   (Some conventions use D_{ij} G_{ij}; project convention follows Tai: Σ D_{ij} G_{ji})

4. DOUBLE-DOT CROSS (dyadic ×̇×̇ dyadic → dyadic):
   D̿ ×̇×̇ G̿ — used in dyadic Green's function identities.

5. UNIT DYADIC (identity):
   I̿ = Σ_i x̂_i x̂_i = x̂x̂ + ŷŷ + ẑẑ
   Property: I̿ · F = F · I̿ = F. Components: (I̿)_{ij} = δ_{ij}.

6. INVERSE: D̿⁻¹ exists iff det(D_{ij}) ≠ 0. D̿ · D̿⁻¹ = D̿⁻¹ · D̿ = I̿.
```

## Classification

```
Symmetric:    D_{ij} = D_{ji}  → 6 independent components. D̿ = D̿^T.
Antisymmetric: D_{ij} = −D_{ji}, D_{ii}=0 → 3 independent components.
              Any antisymmetric dyadic: A̿ = I̿ × a (equivalent to a vector a).
              Cross product with vector: A̿·F = a × F.

Decomposition: Any dyadic = symmetric part + antisymmetric part.
  D̿_sym = ½(D̿ + D̿^T),   D̿_anti = ½(D̿ − D̿^T).

Eigen-dyadic: For symmetric D̿, ∃ three orthogonal eigenvectors û_i:
  D̿ = Σ λ_i û_i û_i   (spectral decomposition)
  where D̿·û_i = λ_i û_i. λ_i are eigenvalues.
```

## Key Identities (General Vector and Dyadic Analysis 1997; Multiforms/Dyadics/EM Media 2015)

```
∇·(D̿·F) = (∇·D̿)·F + D̿^T : ∇F
∇×(D̿·F) = (∇×D̿)·F − (D̿×∇)·F
∇·(I̿ f) = ∇f
∇×(I̿ f) = ∇f × I̿ = −I̿ × ∇f
I̿ : ∇F = ∇·F
```

**Basis-free forms** (Tai 1997, §1.7): The dyadic I̿ is the sole isotropic
dyadic — any isotropic linear map is λ I̿. Key basis-free identities:
```
(a×I̿) · b = a × b          [cross-product map as dyadic]
I̿ × a = −a × I̿             [antisymmetric dyadic from vector]
∇ · (ab) = (∇·a)b + a·(∇b)  [dyadic divergence of dyad ab]
```
These are essential for `em.dyadic_green_function` — the free-space Green
dyadic G̿_e0 = (I̿ + ∇∇/k²)G₀ uses I̿, and source-region corrections use the
depolarization dyadic L̿ (a singular dyadic with det=0).

**Geometric/Clifford algebra connection** (Lindell 2015, Ch.1-2): In the
language of geometric algebra (GA), Maxwell's equations in free space reduce
to ∇F = J where F = E + iζH is a multivector field (bivector + pseudoscalar
parts) and i is the unit pseudoscalar. The dyadic Green function in GA is a
linear mapping between multivectors, unifying the electric and magnetic dyadic
Green functions into a single geometric object. The depolarization dyadic
corresponds to the projection onto the 3D subspace in the GA 4D embedding —
a connection between `mathematics.dyadic_algebra` and the covariant
formulation in `em.covariant_electrodynamics`.

## Edge Cases

- **Non-Cartesian dyadics**: In curvilinear coordinates, unit vectors vary with
  position. Use general dyadic D̿ = Σ D^{ij} g_i g_j where g_i are covariant
  basis vectors. Derivatives require Christoffel symbols.
- **Singular dyadic**: D̿ with det(D_{ij})=0 has no inverse. Common in EM:
  the longitudinal projection dyadic n̂n̂ has det=0.
- **Dyadic Green's functions**: D̿ is a function of two position vectors
  (source and observation). Operations like ∇×G̿(r,r') require care about
  which argument is being differentiated.

## Cross-Domain: When Dyadics Appear in Physics

Every linear constitutive relation or linear differential operator in continuum
physics is fundamentally a dyadic. Recognizing the dyadic structure unifies
seemingly disparate domains:

| Domain | Dyadic | Maps |
|--------|--------|------|
| Electrodynamics | G̿_e (dyadic Green's function) | J(r') → E(r) |
| Plasma | ε̿ (dielectric tensor) | E → D |
| Optics | χ̿^(n) (susceptibility tensor) | E^n → P_NL |
| Elasticity | C̿ (stiffness tensor) | strain ε → stress σ |
| Fluid dynamics | ∇v̿ (velocity gradient dyadic) | position → deformation rate |
| Quantum mechanics | ρ̿ (density matrix) | state vector → ensemble average |

The same dyadic algebra (dot, cross, double-dot, inverse, eigen-decomposition)
applies across all domains — only the physical interpretation of the dyadic
components changes.

## Cross-References

- Tai, *General Vector and Dyadic Analysis* (1997) Ch.1 §1-5, §1-6, §1-7; Ch.7
- Tai, *Dyadic Green Functions in EM Theory* (1993) §1-2
- Lindell, *Multiforms, Dyadics, and EM Media* (2015) Ch.1-2
- mathematics-theorems: mathematics.vector_algebra (parent — vector operations)
- mathematics-theorems: mathematics.vector_green_identities (scalar → vector → dyadic identities)
- electrodynamics: reasoning.em.dyadic_green_function (applies dyadic algebra to EM)
- plasma: plasma.dielectric_response (cold/hot plasma dielectric tensor ε̿ from Vlasov-Maxwell)
- optics: optics.nonlinear_susceptibility (χ̿^(n) tensor symmetries and Kleinman conditions)
- electrodynamics: knowledge.em.crystal_optics (anisotropic ε̿ and wave propagation)
