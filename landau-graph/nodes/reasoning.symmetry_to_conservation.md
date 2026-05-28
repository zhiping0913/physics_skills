---
skill_id: reasoning.symmetry_to_conservation
type: reasoning
summary_50t: >
  Each continuous symmetry of the action implies a conserved quantity.
  This is Noether's theorem in its original mechanical form.
  The seven additive integrals of a closed system are all symmetry-generated.
trigger:
  - found a continuous symmetry of the system
  - need to identify conserved quantities
  - verifying if a quantity is conserved
reasoning_role: symmetry_logic
parent: reasoning.symmetry_drives_physics
children:
  - knowledge.mechanics.energy_conservation
  - knowledge.mechanics.momentum_conservation
  - knowledge.mechanics.angular_momentum_conservation
related:
  - knowledge.mechanics.cyclic_coordinate
retrieval_cost: 1
---

# reasoning.symmetry_to_conservation — Symmetry → Conserved Quantity

## Core Picture

Every continuous symmetry of the action corresponds to a conserved quantity.
This is not an observation — it is a deductive consequence of the Lagrangian
formulation.

For a closed system with s degrees of freedom, there are exactly **2s−1**
independent integrals of motion. Among these, only **seven are additive**
(E, P_x, P_y, P_z, M_x, M_y, M_z) — their values for non-interacting parts
simply sum: Q_total = Σ Q_a. This additivity is why they are "especially
important" (Landau §6): knowing E, P, M before a collision determines them
after, regardless of interaction details. The remaining 2s−8 integrals are
system-specific and not universal.

## Algorithm

**Energy (time translation):**
```
1. For closed system: ∂L/∂t = 0
2. Compute dL/dt = Σ(∂L/∂qᵢ·q̇ᵢ + ∂L/∂q̇ᵢ·q̈ᵢ) using E-L equations
3. d/dt(Σ q̇ᵢ ∂L/∂q̇ᵢ − L) = 0
4. ∴ E = Σ q̇ᵢ pᵢ − L conserved
```
Note: Energy uses the equations of motion directly via dL/dt manipulation,
NOT an infinitesimal symmetry transformation.

**Momentum and Angular Momentum (space symmetries):**
```
1. Identify the continuous symmetry transformation
2. Write the infinitesimal transformation: q → q + δq
3. Compute δL under the transformation:
   Momentum (translation): δL = ε·Σ ∂L/∂rₐ → demand δL = 0
   Angular momentum (rotation): δL = Σ(ṗₐ·δrₐ + pₐ·δvₐ) → δL = 0
4. Use E-L equations: ∂L/∂q = d/dt(∂L/∂q̇)
5. Rearrange to dQ/dt = 0
6. Additivity: Q for non-interacting subsystems = Σ Q_a
```

## Three Canonical Examples (Vol.1 §6-9)

| Symmetry | Transformation | Conserved Quantity |
|----------|---------------|-------------------|
| Time homogeneity | t → t + ε | Energy E = Σ q̇ᵢ pᵢ − L |
| Space homogeneity | rₐ → rₐ + ε | Momentum P = Σ mₐvₐ |
| Space isotropy | r → r + δφ×r | Angular momentum M = Σ rₐ×pₐ |

## Generalized Momentum

For any cyclic coordinate qᵢ (L doesn't depend on it explicitly):
pᵢ = ∂L/∂q̇ᵢ is conserved. This is a special case — the symmetry is
translation in qᵢ, and the conserved quantity is the conjugate momentum.

## Assumptions

- The transformation is CONTINUOUS (discrete symmetries like parity do not
  generate conserved quantities via this mechanism)
- The Lagrangian formalism is valid (forces derivable from potential)
- The system has the stated symmetry (external fields break translation symmetry)

## Edge Cases

- **External fields**: Break homogeneity → P and M components may fail to conserve
  EXCEPT when the field is symmetric along a direction (e.g., uniform field along z
  conserves P_x and P_y)
- **Non-inertial frames**: The symmetry derivation fails because the Lagrangian
  contains explicit time dependence from the frame motion
- **Gauge symmetries**: δL = 0 with δq involving arbitrary functions →
  constraints in the Hamiltonian formalism

## Cross-References

- Landau Vol.1 §6 (Energy), §7 (Momentum), §8 (Center of mass), §9 (Angular momentum)
- Landau Vol.2: Energy-momentum tensor from spacetime translation invariance
- Noether's theorem (general): continuous symmetry → conserved current
- Quantum: conserved quantities → good quantum numbers
