---
skill_id: reasoning.variational_principle
type: reasoning
summary_50t: >
  All fundamental equations of motion follow from δS = 0.
  The Lagrangian is the system's fingerprint — find it,
  and the dynamics are determined.
trigger:
  - constructing equations of motion
  - new physical system without known EOM
  - need to derive dynamics from first principles
reasoning_role: variational_logic
parent: null
children:
  - reasoning.symmetry_to_conservation
  - knowledge.mechanics.lagrangian_free_particle
  - knowledge.mechanics.lagrangian_system
related:
  - reasoning.small_parameter_expansion
retrieval_cost: 1
---

# reasoning.variational_principle — Least Action → Equations of Motion

## Core Picture

A mechanical system is characterized by ONE function — the Lagrangian L(q,q̇,t).
All dynamics are determined by the single requirement that the action S = ∫L dt
is stationary against all variations that vanish at the endpoints.

This is NOT a mathematical trick. It is the most general formulation of classical
mechanics. All other approaches (Newton, Hamilton, Hamilton-Jacobi) are derived
from this one principle.

## Key Equations

```
S = ∫ L(q, q̇, t) dt
δS = 0  →  d/dt(∂L/∂q̇ᵢ) − ∂L/∂qᵢ = 0
```
Euler-Lagrange equations. s second-order ODEs for s degrees of freedom.

## The Lagrangian's Non-Uniqueness

L is defined only up to:
1. A total time derivative: L' = L + dF(q,t)/dt gives identical EOM
2. A multiplicative constant (fixed by additivity across subsystems)

## Assumptions

- The system is characterized by generalized coordinates q and velocities q̇
- **L depends only on q and q̇, NOT on higher derivatives** (q̈, q⃛, ...).
  This is because classical mechanics assumes the state at one time is fully
  determined by (q,q̇) alone. This assumption fails for:
  - Radiation reaction (Abraham-Lorentz force depends on acceleration)
  - Effective field theories with higher-derivative terms
  - Non-local theories
- Forces are derivable from a potential (no dissipation → see knowledge.mechanics.dissipation)
- The action has a stationary point (not necessarily a minimum — see below)

## The Minimum vs Extremum Issue

Landau §2 footnote: "принцип наименьшего действия не всегда справедлив
для всей траектории в целом, а лишь для каждого из достаточно малых
ее участков." The action is only guaranteed to be MINIMAL for small segments
of the trajectory. For the full trajectory, it may be merely EXTREMAL.
This becomes crucial in relativistic mechanics (Vol.2 §8) where
S = −mc∫ds: the interval ∫ds is MAXIMIZED along a straight worldline,
so the negative sign makes S MINIMIZED. The sign of the action is chosen
so that S has a true minimum for small path segments.

## Edge Cases

- **Non-holonomic constraints**: Cannot be handled by simple L alone — need
  Lagrange multipliers. The variational derivation still works: constraints
  f_i(q,q̇) = 0 mean δq is NOT fully arbitrary → add λ_i f_i terms.
- **Dissipative systems**: Forces not derivable from potential → need
  Rayleigh dissipation function
- **Minimum vs extremum** (see above): The action may be extremal but not
  minimal for the full trajectory. Only small segments are guaranteed minima.

## Misconceptions

- "L = T − U" is NOT the definition of the Lagrangian. It is a CONSEQUENCE
  of Galilean invariance applied to a system with velocity-independent forces.
  The true definition is: L is that function whose action integral is stationary.

## Cross-References

- Landau Vol.1 §2 (derivation of Euler-Lagrange)
- Landau Vol.1 §4 (constructing L from Galilean invariance — see reasoning.symmetry_to_lagrangian)
- Landau Vol.2 §2 (relativistic action)
- See wiki: action-principle for plasma applications
