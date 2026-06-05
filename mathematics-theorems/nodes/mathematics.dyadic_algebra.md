---
skill_id: mathematics.dyadic_algebra
type: reasoning
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

## Algorithm — Products and Operations

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

## Key Identities

```
∇·(D̿·F) = (∇·D̿)·F + D̿^T : ∇F
∇×(D̿·F) = (∇×D̿)·F − (D̿×∇)·F
∇·(I̿ f) = ∇f
∇×(I̿ f) = ∇f × I̿ = −I̿ × ∇f
I̿ : ∇F = ∇·F
```

## Edge Cases

- **Non-Cartesian dyadics**: In curvilinear coordinates, unit vectors vary with
  position. Use general dyadic D̿ = Σ D^{ij} g_i g_j where g_i are covariant
  basis vectors. Derivatives require Christoffel symbols.
- **Singular dyadic**: D̿ with det(D_{ij})=0 has no inverse. Common in EM:
  the longitudinal projection dyadic n̂n̂ has det=0.
- **Dyadic Green's functions**: D̿ is a function of two position vectors
  (source and observation). Operations like ∇×G̿(r,r') require care about
  which argument is being differentiated.

## Cross-References

- Tai, *General Vector and Dyadic Analysis* (1997) Ch.1 §1-5, §1-6, §1-7; Ch.7
- Tai, *Dyadic Green Functions in EM Theory* (1993) §1-2
- Lindell, *Multiforms, Dyadics, and EM Media* (2015) Ch.1-2
- mathematics-theorems: mathematics.vector_algebra (parent — vector operations)
- mathematics-theorems: mathematics.vector_green_identities (scalar → vector → dyadic identities)
- electrodynamics: reasoning.em.dyadic_green_function (applies dyadic algebra to EM)
