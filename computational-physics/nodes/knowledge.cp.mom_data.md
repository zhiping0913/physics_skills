---
skill_id: knowledge.cp.mom_data
type: knowledge
summary_50t: >
  MoM reference data: EFIE/MFIE/CFIE condition numbers vs frequency.
  RWG basis properties (divergence, charge neutrality). Matrix fill
  singularity extraction methods. MLFMA complexity O(N log N). Common
  pitfalls: interior resonance, low-frequency breakdown, mesh density.
retrieval_cost: 1
---

# knowledge.cp.mom_data — MoM Reference

## Basis Functions

| Type | Support | Divergence | Used For |
|------|---------|-----------|----------|
| Pulse (1D) | One segment | δ-like at endpoints | Wire MoM |
| Triangle (1D) | Two adjacent segments | Constant on segments | Wire MoM |
| RWG (3D surface) | Two adjacent triangles | Constant on each triangle | Surface EFIE/MFIE |
| Roof-top (2D planar) | Four adjacent rectangles | Constant per rectangle | Microstrip, planar |

**RWG (Rao-Wilton-Glisson, 1982)**: The standard surface basis.
- Edge n connects triangles T_n^+ and T_n^-. ℓ_n = edge length.
- f_n(r) = (ℓ_n/(2A_n^±))(r − r_n^±) on T_n^±; zero elsewhere.
- Key property: ∇_s·f_n = ±ℓ_n/A_n^± (constant divergence) → charge neutrality
  automatically satisfied: total charge on each triangle pair = 0.
- Mesh requirement: edges must match; each interior edge has exactly 2 triangles.

## Integral Equations Compared

| Equation | Unknown | Condition No. (low freq) | Interior Resonance | Notes |
|----------|---------|------------------------|-------------------|-------|
| EFIE | J | ∝ 1/k (ill-cond.) | YES | Works for open & closed |
| MFIE | J | ~const | YES | Closed surfaces only |
| CFIE | J | ~const | NO | α≈0.2-0.5 recommended |
| PMCHWT | J, M | ∝ 1/k | NO | Dielectric bodies |

**Interior resonance fix**: CFIE = α EFIE + (1−α)η₀ MFIE. For any α≠0,
the CFIE operator is non-singular at all frequencies.

## Matrix Fill: Singularity Extraction

Z_{mn} requires integrating 1/R and 1/R³ singularities. Triangle pairs
share edges/vertices → singularity.

**Analytical extraction**: For the scalar potential 1/R integral over a
triangle: use closed-form formulas (Wilton et al., 1984; Graglia 1993).
The self-term (m=n) is completely analytical for planar triangles.

## MLFMA Complexity

| N (unknowns) | Direct (O(N³)) | MLFMA (O(N log N)) |
|-------------|----------------|---------------------|
| 10³ | 1 sec | 1 sec |
| 10⁴ | 1000 sec | 10 sec |
| 10⁵ | 10⁶ sec | 100 sec |
| 10⁶ | infeasible | 1000 sec |

## Common Pitfalls

- **Mesh too coarse**: Δ ≤ λ/10 for current accuracy. RWG needs ~300 unknowns/λ².
- **Low-frequency breakdown**: Use loop-star or A-Φ formulation.
- **RWG charge cancellation**: Both triangles of edge pair must be present.
