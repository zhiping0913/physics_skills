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
  determined by (q,q̇) alone.
- Forces are derivable from a potential (no dissipation)
- The action has a stationary point (not necessarily a minimum — see below)

## The Minimum vs Extremum Issue

Landau §2 footnote: the action is only guaranteed to be MINIMAL for small segments
of the trajectory. For the full trajectory, it may be merely EXTREMAL.
This becomes crucial in relativistic mechanics (Vol.2 §8) where
S = −mc∫ds: the interval ∫ds is MAXIMIZED along a straight worldline,
so the negative sign makes S MINIMIZED.

## Edge Cases

- **Non-holonomic constraints**: Cannot be handled by simple L alone — need
  Lagrange multipliers.
- **Dissipative systems**: Forces not derivable from potential → need
  Rayleigh dissipation function
- **Minimum vs extremum**: The action may be extremal but not minimal for the
  full trajectory. Only small segments are guaranteed minima.

## Misconceptions

- "L = T − U" is NOT the definition of the Lagrangian. It is a CONSEQUENCE
  of Galilean invariance applied to a system with velocity-independent forces.
  The true definition is: L is that function whose action integral is stationary.

## Constructing L from Symmetry: The Algorithm (§4-§5)

The variational principle alone doesn't tell you HOW to find L.
The most common gap reported by agents: they know δS=0 but can't construct L.

### Free Particle: Galilean Invariance → L = ½mv² (§4)

```
1. HOMOGENEITY + ISOTROPY: Free particle in inertial frame → L depends
   only on speed: L = L(v²) (no preferred position, direction, or time).
2. GALILEAN RELATIVITY: EOM must be the same in all inertial frames.
   Transform to frame K' moving with infinitesimal velocity ε:
   v' = v + ε → L' = L(v² + 2v·ε + ε²) ≈ L(v²) + (∂L/∂v²)·2v·ε
3. NON-UNIQUENESS OF L: L' may differ from L by at most a total time
   derivative: L' = L + dF/dt. This is the CONSTRAINT that fixes L.
4. The term (∂L/∂v²)·2v·ε must be a total time derivative.
   For this to hold for arbitrary ε, ∂L/∂v² must be CONSTANT.
5. Therefore L = const·v². Define const = m/2 → L = ½mv².
6. ADDITIVITY: For non-interacting particles L = Σ ½mₐvₐ².
   This fixes the mass ratios (only ratios have physical meaning).
7. SIGN: m > 0 because otherwise S would have no minimum (§4 footnote).
```

**Key insight**: The "L non-uniqueness" (step 3) is not a bug — it's the
essential tool that FIXES the functional form. Without this step, any
function of v² would satisfy homogeneity and isotropy.

### Interacting Particles: L = T − U (§5)

```
1. For a closed system of interacting particles: add a function −U(r₁,r₂,…)
   to the free-particle Lagrangian: L = Σ ½mₐvₐ² − U(r₁,r₂,…)
2. U depends only on coordinates (instantaneous positions).
   This is forced by Galilean relativity + absolute time (§5):
   if interaction propagated at finite speed, laws would differ across frames.
3. E-L gives: mₐdvₐ/dt = −∂U/∂rₐ (Newton's 2nd law with F = −∇U).
```

The sign convention (−U) ensures E = T + U with T ≥ 0.

### For Relativistic Particles

Same constructive approach: homogeneity + isotropy → L = f(v²).
Lorentz invariance (instead of Galilean) → L = −mc²√(1−v²/c²).
See `reasoning.lorentz_invariance_to_action`.

## Cross-References

- Landau Vol.1 §2 (Euler-Lagrange), §4-§5 (constructing L)
- Landau Vol.2 §2 (relativistic action)
- reasoning.lorentz_invariance_to_action (relativistic L construction)
- reasoning.symmetry_drives_physics (parent pattern)
