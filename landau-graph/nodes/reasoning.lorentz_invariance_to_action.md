---
skill_id: reasoning.lorentz_invariance_to_action
type: reasoning
summary_50t: >
  The action must be a Lorentz scalar. For a free particle, the only scalar
  from its worldline is ∫ds → S = −mc∫ds → L = −mc²√(1−v²/c²).
  Same template as Vol.1 T1, but with Lorentz group replacing Galilean.
trigger:
  - constructing relativistic Lagrangian
  - need action invariant under Lorentz transformations
  - generalizing classical mechanics to relativistic domain
reasoning_role: symmetry_to_lagrangian
parent: reasoning.symmetry_drives_physics
children:
  - knowledge.relativity.action_free_particle
  - knowledge.relativity.energy_momentum
related:
  - knowledge.mechanics.lagrangian_free_particle
retrieval_cost: 1
---

# reasoning.lorentz_invariance_to_action — Lorentz Invariance → Relativistic Action

## Core Picture

The reasoning template from Vol.1 §4 (symmetry → Lagrangian form) generalizes
directly: instead of Galilean invariance, demand Lorentz invariance.

The action S must be a Lorentz scalar (invariant under Lorentz transformations).
The only scalar that can be built from a particle's worldline alone is the
interval ds, or α·ds. Therefore S = −α∫ds. The negative sign is chosen so that
S has a minimum along the straight worldline (analogous to the m>0 argument).

Fix α by matching to the classical limit v≪c: L = −αc√(1−v²/c²) ≈ −αc + αv²/2c.
Dropping the constant and demanding L → mv²/2 gives α = mc.

## Key Equations

```
S = −mc ∫ ds                      action (Lorentz scalar)
L = −mc² √(1 − v²/c²)             Lagrangian
p = ∂L/∂v = mv/√(1−v²/c²)        momentum
E = p·v − L = mc²/√(1−v²/c²)     energy
E²/c² = p² + m²c²                  mass shell condition
```

## Contrast with Galilean Case (Vol.1 §4)

| Aspect | Galilean (Vol.1) | Lorentz (Vol.2) |
|--------|-----------------|-----------------|
| Invariant | t (absolute time) | ds² = c²dt²−dr² |
| Symmetry group | Galilean | Lorentz (SO(3,1)) |
| L form | mv²/2 | −mc²√(1−v²/c²) |
| Limit | exact at v≪c | recovers mv²/2 at v≪c |
| Mass-energy | E = T (kinetic only) | E₀ = mc² (rest energy) |

## Key Insight

**The sign is forced by the minimum action principle**. For a free particle,
the interval ∫ds is MAXIMIZED along the straight worldline (Vol.1 §3).
Therefore the action integral with positive sign would have no minimum.
The negative sign S = −mc∫ds makes S MINIMIZED — the same logic as Vol.1 §2
where Landau notes the action is only guaranteed minimal for small segments
of the trajectory. The relativistic case is where this distinction between
minimum and extremum becomes physically decisive.

## Cross-References
- Landau Vol.2 §8 (action), §9 (energy-momentum)
- Landau Vol.1 §4 (Galilean → L = mv²/2) — same template
- Landau Vol.2 §27 (action for EM field)
