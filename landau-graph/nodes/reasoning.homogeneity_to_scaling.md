---
skill_id: reasoning.homogeneity_to_scaling
type: reasoning
summary_50t: >
  If the potential is homogeneous of degree k, all mechanical quantities
  scale as powers of the length ratio — no integration needed.
  This yields the virial theorem: 2⟨T⟩ = k⟨U⟩.
trigger:
  - U is a homogeneous function of coordinates
  - need scaling relations without solving EOM
  - checking dimensional consistency of a physical argument
reasoning_role: scaling_argument
parent: reasoning.variational_principle
children:
related:
  - knowledge.mechanics.kepler_problem
retrieval_cost: 1
---

# reasoning.homogeneity_to_scaling — Homogeneous Potential → Scaling Relations

## Core Picture

If U(αr₁,...,αr_N) = αᵏ U(r₁,...,r_N), then the equations of motion admit
geometrically similar trajectories. By scaling coordinates (r → αr) and
time (t → βt), and demanding the Lagrangian transform by an overall
constant factor, you get β = α^(1−k/2). All mechanical quantities then
follow definite power laws.

This is pure dimensional analysis elevated to physical law — the homogeneity
degree k replaces the usual dimensional constraints.

## Key Equations

```
t'/t = (l'/l)^(1−k/2)           time scaling
v'/v = (l'/l)^(k/2)             velocity scaling
E'/E = (l'/l)^k                 energy scaling
M'/M = (l'/l)^(1+k/2)           angular momentum scaling
```

## Virial Theorem

For bounded motion, the time average of Σ pₐ·rₐ vanishes, yielding:
```
2⟨T⟩ = ⟨Σ rₐ·∂U/∂rₐ⟩
```
If U is homogeneous of degree k:
```
2⟨T⟩ = k⟨U⟩
⟨U⟩ = 2E/(k+2),  ⟨T⟩ = kE/(k+2)
```

## Canonical Cases

| k | System | Scaling | Virial |
|---|--------|---------|--------|
| 2 | Harmonic oscillator | Period independent of amplitude | ⟨T⟩ = ⟨U⟩ |
| 1 | Uniform gravity | t ∝ √h (free fall) | ⟨T⟩ = ½E |
| −1 | Coulomb/Newton | T² ∝ a³ (Kepler 3rd) | 2⟨T⟩ = −⟨U⟩, E = −⟨T⟩ |

## Edge Cases

- **U not homogeneous**: No universal scaling. Different regimes may emerge.
- **Unbounded motion**: Virial theorem derivation requires Σ pₐ·rₐ bounded.
- **k = −2**: β ∝ α² — qualitatively different from all other k. The time
  scales quadratically with the length scale. Example: potential between
  two parallel line charges.
- **k = 0**: β ∝ α — time scales linearly with length. Trivial case.

## Cross-References

- Landau Vol.1 §10 (Mechanical similarity)
- Plasma: virial theorem for Vlasov-Poisson equilibrium
- Astrophysics: virial mass estimator for galaxies/clusters
- **Connection to dimensional analysis**: This is the Π-theorem (Buckingham)
  in mechanical form. With 3 parameters (m,l,E) of dimensions [M,L,T],
  there is exactly 1 independent dimensionless combination. The homogeneity
  degree k replaces the usual dimensional constraints when the potential
  has no fixed scale.
