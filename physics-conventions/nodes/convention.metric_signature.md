---
skill_id: convention.metric_signature
type: convention
summary_50t: >
  Metric: (−+++). ds²=−c²dt²+dx²+dy²+dz². 4-gradient ∂_μ=(∂_t/c,∇), ∂^μ=(−∂_t/c,∇).
  4-potential A^μ=(φ/c,A), A_μ=(−φ/c,A). d'Alembertian □=−∂_t²/c²+∇². Landau uses
  (+−−−): flip sign of every g^μν contraction to convert.
---

# Metric signature convention

**Project default**: (−+++), i.e., timelike component negative, spacelike
positive. This is the standard in Stix, Jackson, most GR textbooks (MTW), and
the plasma/electrodynamics community.

## Key 4-vectors and operators

**4-interval**:
```
ds² = −c² dt² + dx² + dy² + dz² = g_μν dx^μ dx^ν
```

**4-gradient**:
```
∂_μ = (∂_t/c, ∇)          covariant
∂^μ = (−∂_t/c, ∇)         contravariant
```

**4-potential**:
```
A^μ = (φ/c, A)            contravariant
A_μ = (−φ/c, A)           covariant
```

**d'Alembertian**:
```
□ = ∂_μ ∂^μ = −∂_t²/c² + ∇²
```

**4-velocity**:
```
u^μ = (γc, γv)            contravariant
u_μ = (−γc, γv)           covariant
u^μ u_μ = −c²
```

**4-momentum**:
```
p^μ = (E/c, p)            contravariant
p_μ = (−E/c, p)           covariant
p^μ p_μ = −m²c²
```

## Conversion to Landau (+−−−)

Landau-Lifshitz uses metric (+−−−), i.e., ds² = c²dt² − dx² − dy² − dz².
When citing a Landau-derived formula in a project (downstream) node:

1. **Flip the sign of every g^μν contraction**. In (−+++):
   u^μ u_μ = −c². In (+−−−): u^μ u_μ = +c².
2. **∂_μ differs by a sign on the time component**. In (+−−−):
   ∂_μ = (∂_t/c, −∇) instead of (∂_t/c, ∇).
3. **Lagrangian density sign**: L for the EM field changes sign.
   In (−+++): L_EM = −F_μν F^μν / (4μ₀). In (+−−−): L_EM = −F_μν F^μν / (16π).

## When conversion is unnecessary

Most landau-graph results are dimensional scaling laws or conservation
arguments. The metric sign only matters when **4-vector contractions**
appear explicitly (radiation 4-momentum, energy-momentum tensor, action
principle derivations). For 3-vector formulas no conversion is needed.

## References

Jackson §11.6–11.7 (GR introduction, −+++), Landau Vol 2 §82 (metric +−−−),
MTW Box 1.2 (signature conventions), Stix §2 (relativistic plasma, uses −+++).
