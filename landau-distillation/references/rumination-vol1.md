# Volume 1 Rumination Report

Date: 2026-05-26. Re-read original with graph nodes loaded.

## Issues Found

### HIGH: symmetry_to_conservation — Missing 2s-1 counting
Landau §6 states a closed system with s DOF has exactly 2s-1 integrals, but only
7 (E,P,M) are ADDITIVE. Additivity is the defining property of "important" 
conserved quantities — enables collision problems. Template missed this.

### HIGH: symmetry_to_conservation — Energy derivation differs
Energy uses dL/dt manipulation; momentum/angular momentum use δL = 0 from 
infinitesimal transformation. These are structurally different derivations.

### MEDIUM: variational_principle — Minimum vs Extremum
Landau's footnote: action may be extremal (not minimal) for full trajectory.
This matters in relativistic case (Vol.2) where action is a maximum.

### MEDIUM: adiabatic_invariance — Requires integrability
Unperturbed system must be integrable (orbit p(q;E,λ) must exist).
For non-integrable systems, adiabatic invariant concept fails.

### MEDIUM: adiabatic_invariance — Averaging over fictitious orbit
Landau: "усреднение производится по такому движению системы, какое имело 
бы место при заданном постоянном значении λ." The average is over the 
λ=const orbit, not the true orbit.

### LOW: homogeneity_to_scaling — Missing k=-2 case, Π-theorem connection

## Hidden Parent Nodes Found

### reasoning.timescale_hierarchy
Children: adiabatic_invariance + small_parameter_expansion
Both separate fast/slow dynamics.

### reasoning.symmetry_drives_physics
Children: symmetry_to_conservation (Vol.1) + lorentz_invariance_to_action (Vol.2) 
+ gauge_invariance_to_field_tensor (Vol.2)
All use symmetry as CONSTRUCTIVE tool, not observation.

## Cross-Volume Connections to Add

- adiabatic_invariance (Vol.1) → WKB/quantization (Vol.3)
- small_parameter (Vol.1) → multipole_expansion (Vol.2) — both scale separation
- homogeneity_scaling (Vol.1) → Reynolds similarity (Vol.6) — both Π-theorem
