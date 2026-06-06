---
skill_id: knowledge.cp.fem_data
type: knowledge
summary_50t: >
  FEM reference: element types (nodal, edge, face), shape function orders
  (p=1,2,3), quadrature rules, matrix properties (sparsity, conditioning),
  sparse direct solver memory scaling. hp-adaptivity error indicators.
retrieval_cost: 1
---

# knowledge.cp.fem_data — FEM Reference

## Element Types

| Element | Unknowns per element | Continuity | Spurious Modes? |
|---------|---------------------|------------|-----------------|
| Nodal (Lagrange, p=1) | 4 (tet) / 3 (tri) | All E components | YES — must use edge elements |
| Edge (Nédélec, p=1) | 6 (tet) / 3 (tri) | Tangential only | NO |
| Edge (Nédélec, p=2) | 20 (tet) / 8 (tri) | Tangential only | NO |
| Face (Raviart-Thomas, p=1) | 4 (tet) | Normal only | For B, D fields |

For Maxwell: ALWAYS use edge elements (Nédélec, Whitney 1-forms).
For electrostatic (scalar): nodal elements are fine.

## Edge Element Hierarchy (Whitney Complex)

```
p=1 (Whitney 1-form):  N_{ij} = λ_i ∇λ_j − λ_j ∇λ_i       (edge i→j)
p=2 (Nédélec):         20 DoFs: 2 per edge, 2 per face
```
λ_i = barycentric coordinate on tetrahedron.

## Matrix Properties

| Property | Value |
|----------|-------|
| Sparsity | ~20-50 nonzeros per row (tet, p=1); ~150 (p=2) |
| Symmetry | Complex symmetric for lossless (K real, M real); general for lossy |
| Condition no. | ∝ 1/h² for K; ~const for M. Combined: κ(A) ~ (k₀h)⁻² for low freq |
| Null space of K | Gradient fields (∇φ). Tree-cotree gauge removes |

## Sparse Direct Solver Memory

| N (tet, p=1) | Fill-in factor | Memory (GB) |
|-------------|---------------|-------------|
| 10⁵ | ~500 | 4 |
| 5×10⁵ | ~1000 | 40 |
| 10⁶ | ~1500 | 120 |

Beyond ~5×10⁵: switch to iterative (preconditioned CG/GMRES) or domain decomposition.

## hp-Adaptivity

- **h-refinement**: Subdivide elements → more elements, same order.
- **p-refinement**: Increase polynomial order → exponential convergence for smooth solutions.
- **Error indicator**: Jump in n̂×H across element faces (residual-based) guides
  which elements to refine.

## Common Pitfalls

- **Using nodal elements for curl-curl**: Produces spurious modes with ∇·E≠0.
- **PEC enforcement**: Remove DoFs on PEC surfaces BEFORE assembly.
- **Low-frequency breakdown**: As k₀→0, the curl-curl part dominates → system singular.
