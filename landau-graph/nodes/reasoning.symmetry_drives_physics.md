---
skill_id: reasoning.symmetry_drives_physics
type: reasoning
summary_50t: >
  Symmetry is not an observation — it is a CONSTRUCTIVE tool that
  dictates the form of physical law. Landau's deepest methodological
  principle across all volumes.
trigger:
  - constructing physical law from first principles
  - need to constrain unknown Lagrangian/Hamiltonian/action
  - any problem where symmetry can REPLACE guesswork
reasoning_role: symmetry_as_constructive_principle
parent: reasoning.variational_principle
children:
  - reasoning.symmetry_to_conservation
  - reasoning.lorentz_invariance_to_action
  - reasoning.gauge_invariance_to_field_tensor
retrieval_cost: 1
---

# reasoning.symmetry_drives_physics — Symmetry as Constructive Principle

## Core Picture

Landau never says "we observe that energy is conserved, therefore..." 
Instead, he says: "space and time have these symmetry properties —
therefore the Lagrangian MUST have this form — and therefore these
quantities are conserved."

Symmetry is not a classification tool. It is a DERIVATION tool.
This is the single most important methodological insight in the
Landau-Lifshitz course.

## Instances Across Volumes

| Volume | Symmetry | What It Derives |
|--------|----------|----------------|
| Vol.1 §4 | Galilean invariance | L = mv²/2 |
| Vol.1 §6-9 | Homogeneity/isotropy of spacetime | E, P, M conservation |
| Vol.2 §4 | Lorentz invariance | Lorentz transformation |
| Vol.2 §8 | Lorentz invariance of action | S = −mc∫ds, L = −mc²√(1−v²/c²) |
| Vol.2 §18 | Gauge invariance | F_ik must be fundamental field |
| Vol.3 §17 | Galilean + homogeneity | Ĥ = p̂²/2m (quantum) |
| Vol.6 §15 | Isotropy + Galilean | Navier-Stokes stress tensor form |

## The Pattern

```
1. Identify the symmetry group of the physical situation
2. Write the most general object (L, H, action, tensor) compatible with it
3. The symmetry constrains the functional form
4. Additional constraints (additivity, positive-definiteness) fix constants
5. The resulting physical law is DERIVED, not postulated
```

## When This Method is Most Powerful

- Unknown systems: when you don't know the dynamics but know the symmetries
- Unification: when different phenomena share the same symmetry → same math
- Generalization: Galilean → Lorentz is the same logic applied to larger group

## Cross-References
- All volumes of Landau-Lifshitz
- This is arguably THE unifying reasoning pattern of the entire course
