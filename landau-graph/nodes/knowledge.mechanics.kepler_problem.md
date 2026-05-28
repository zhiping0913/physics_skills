---
skill_id: knowledge.mechanics.kepler_problem
type: knowledge
summary_50t: >
  U = −α/r. Orbits are conic sections. E<0: elliptical (bound).
  T² ∝ a³ (3rd law). The Runge-Lenz vector A = p×M − mα r/r is conserved.
trigger:
  - inverse-square force law
  - gravitational or Coulomb two-body problem
reasoning_role: exact_solution
parent: knowledge.mechanics.central_field_effective
related:
  - reasoning.homogeneity_to_scaling
retrieval_cost: 1
---

# knowledge.mechanics.kepler_problem

**Key equations**:
```
U = −α/r
Orbit: p/r = 1 + e cos φ
  p = M²/(mα)          semi-latus rectum
  e = √[1 + 2EM²/(mα²)] eccentricity
  E = −mα²(1−e²)/(2M²)

Bound (E<0): ellipse,  a = α/(2|E|),  T² = 4π²ma³/α (3rd law)
Unbound (E>0): hyperbola
E=0: parabola (escape)
```

**Hidden symmetry**: Runge-Lenz vector A = p×M − mα r/r is conserved.
This is why the orbit closes — an extra constant of motion beyond E and M.

**Reduced mass**: Two-body → one-body with μ = m₁m₂/(m₁+m₂).

**Action variables**: I_φ = M,  I_r = −M + α√(m/2|E|),
E = −mα²/[2(I_r+I_φ)²]. Degenerate: ω_r = ω_φ.

- Landau Vol.1 §15
