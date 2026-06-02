---
skill_id: reasoning.hidden_symmetry
type: reasoning
summary_50t: >
  When frequencies are degenerate (ω_i/ω_j ∈ ℚ for all actions),
  extra conserved quantities beyond the s action variables emerge from
  the phase-space orbit structure — not from Lagrangian symmetries.
  Degeneracy → extra integral → closed orbits. Canonical: Runge-Lenz.
trigger:
  - system has more conserved quantities than obvious symmetries
  - closed orbits where theory predicts they should be open
  - degeneracy in action-angle frequencies
reasoning_role: degeneracy_as_hidden_symmetry
parent: reasoning.symmetry_drives_physics
children:
  - knowledge.mechanics.kepler_problem
  - knowledge.mechanics.action_angle_variables
retrieval_cost: 1
---

# reasoning.hidden_symmetry — Degeneracy → Extra Conserved Quantity

## Core Picture

Manifest symmetries (time/space translation, rotation) produce conserved
quantities via Noether's theorem: E, P, M. But some systems have MORE
conserved quantities than these — quantities that do NOT correspond to
any obvious continuous symmetry of the Lagrangian in configuration space.

These are **hidden symmetries**. Their origin is not in coordinate
transformations but in the **degeneracy of frequencies** in action-angle
variables: when ω_i = ω_j (or rational ratio) for ALL values of the
actions, the Hamiltonian depends on FEWER independent combinations of
the action variables than there are degrees of freedom. This leaves room
for extra single-valued integrals of motion.

## Manifest vs Hidden Symmetry

| | Manifest (Noether) | Hidden (Degeneracy) |
|---|---|---|
| **Origin** | Symmetry of L in configuration space | Degeneracy in phase-space orbit structure |
| **Method** | Infinitesimal coordinate transformation | Action-angle frequency analysis |
| **Output** | E, P, M (additive, universal) | Runge-Lenz vector (system-specific) |
| **Domain** | ALL closed systems | ONLY special potentials (1/r, r²) |

The two are **complementary**, not subordinate. Manifest symmetry is the
rule; hidden symmetry is the exceptional case — but when it occurs, it
has profound consequences (closed orbits, superintegrability, multiple
coordinate separability).

## Algorithm: From Closed Orbits to Degeneracy

```
1. OBSERVE: Orbits are closed for ALL bound states.
   → For a 2-DOF central-field system, closed orbits require an extra
     conserved quantity beyond E and M (2 integrals but need 3).
   → Bertrand's theorem: only U ∝ 1/r and U ∝ r² have this property (§14).

2. DERIVE THE EXTRA QUANTITY DIRECTLY:
   For U = −α/r (Kepler):  A = p×M − mα r̂  satisfies dA/dt = 0.
   Verify by direct differentiation using ṗ = −αr/r³.
   A is a single-valued function of state (однозначная функция).

3. UNDERSTAND THE ORIGIN (action-angle analysis, §52):
   Compute action variables: I_φ = M,  I_r = −M + α√(m/2|E|).
   Energy: E = −mα² / 2(I_r + I_φ)².
   Frequencies: ω_r = ∂E/∂I_r = ω_φ = ∂E/∂I_φ.
   → DEGENERACY: both frequencies equal for ALL (I_r, I_φ).

4. DEGENERACY → EXTRA INTEGRAL (§52):
   In general, s DOFs → s single-valued integrals (the I_i).
   Degeneracy: E depends on FEWER than s independent combinations
   of the I_i → extra s−k single-valued integrals exist.
   For Kepler (s=2, k=1): the combination w_r − w_φ, though
   multi-valued, yields single-valued functions when inserted into
   trigonometric expressions → Runge-Lenz vector.

5. DEGENERACY → MULTIPLE SEPARABILITY (§52):
   "Degenerate motions admit complete separation of variables with
   different, not just one definite, choice of coordinates."
   Kepler separates in BOTH spherical AND parabolic coordinates —
   a direct consequence of the extra integral.
```

## The Runge-Lenz Vector (Landau §15)

For U = −α/r:  **A = p × M − mα r̂**

Properties:
- A is conserved (dA/dt = 0)
- A·M = 0 (lies in the orbit plane)
- |A| = mαe (magnitude = eccentricity × mα)
- A points from the focus to the perihelion
- A² = m²α² + 2mE M² (relates energy, eccentricity, angular momentum)

## Counterexample: Non-Degenerate Potential

For U = −α/r^(1.1) (generic, non-degenerate):
- ω_r ≠ ω_φ (incommensurate for generic I values)
- Orbits are NOT closed — they fill an annulus densely
- No extra single-valued integral beyond E and M
- Only ONE coordinate system permits separation (radial)

This is the GENERIC case. Hidden symmetry is EXCEPTIONAL.

## Edge Cases

- **Perturbed Kepler**: Small deviations from 1/r destroy exact degeneracy
  → orbits precess → Runge-Lenz vector slowly rotates. The precession rate
  is the measure of symmetry breaking.
- **Harmonic oscillator**: U ∝ r² has its own hidden symmetry (Fradkin tensor,
  SU(3) in 2D). The degeneracy pattern is different from Kepler.
- **Accidental vs systematic degeneracy**: True hidden symmetry means
  degeneracy for ALL values of the actions, not just at special points.

## Scope Boundary (What This Node Does NOT Cover)

- SO(4) group structure of Kepler (Fock 1935) — requires group theory beyond Landau Vol.1
- KAM theory (fate of tori under perturbation) — post-Landau
- Bertrand's theorem proof — mathematical theorem, see `mathematics-theorems`
- Quantum hidden symmetry (hydrogen atom SO(4) degeneracy) — requires Vol.3

## Cross-References

- Landau Vol.1 §15 (Runge-Lenz vector), §52 (degeneracy in action-angle variables)
- reasoning.symmetry_to_conservation (manifest Noether — complementary pattern)
- reasoning.canonical_transformation (prerequisite: action-angle variables)
- reasoning.adiabatic_invariance (analogy: both find non-obvious conserved quantities)
- knowledge.mechanics.kepler_problem (Runge-Lenz vector as concrete instance)
- knowledge.mechanics.action_angle_variables (degeneracy condition ω_i = ω_j)
