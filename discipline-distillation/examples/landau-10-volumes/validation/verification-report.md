# Round 1 Improvement Verification Report

Date: 2026-05-28. Cross-check: updated nodes vs 60 deepseek + ~30 opus confusions.

## Summary

| Category | Count | Description |
|----------|-------|-------------|
| SOLVED | ~25 | Node improvements directly address the confusion |
| IMPROVED | ~10 | Better context/connection, but not a complete solution |
| NOT ADDRESSED | ~15 | Requires new nodes or fundamentally new content |
| OUT OF SCOPE | ~10 | Mathematical details, conventions, or advanced theorems |

---

## SOLVED — Node Improvements That Work

### Vol.1: Lagrangian Construction (C1-C4, opus issue 8)
Deepseek: "I cannot construct L=½mv² from δS=0 alone."
→ `variational_principle` now has full 7-step Galilean→L algorithm (§4).
Deepseek: "momentum formula has unstated dependency on L form."
→ `symmetry_to_conservation` now has "Hidden Dependencies" section.
Opus: "Hamilton equations assumed, not derived."
→ `canonical_transformation` now has Legendre transform universal table.

### Vol.2: LW Fields (C11)
Deepseek: "reasoning node gives LW potential but NOT the complete field expression."
→ `retarded_green_function` now has full "LW Potentials→Fields" section
with κ denominator, 1/R² vs 1/R decomposition, and relativistic beaming.

### Vol.3: Schrödinger as Postulate (C1)
Deepseek: "The SE is NOT derived — it's a new postulate."
→ `classical_to_quantum` now has "Epistemological shift" section
explicitly listing 4 new postulates and citing Landau's §17 footnote.

### Vol.5: 1/N! and Identical Particles (C1)
Deepseek: "The 1/N! factor — WHY?"
→ `quantum_superposition` now has "Identical particles" section covering
Ψ(1,2)=±Ψ(2,1), Pauli exclusion, Slater determinants, exchange energy.

### Cross-Volume: Constitutive Trinity (B-8, P0)
Gap analysis: "Single biggest cross-volume pattern."
→ `constitutive_relation` now has "Cross-volume trinity" with explicit
formulas for viscous stress, Hooke's law, dielectric, and conductivity.

### Cross-Volume: Linear Response (A4, P2)
Opus: "Pattern applies to ALL linear susceptibilities."
→ `linear_response_general` (new node) is the unified entry point.
`causality_to_analyticity` now references 7 specific susceptibility types.

### Cross-Volume: Equilibrium as Extremum (A1)
Opus: "No single node captures δS=0 = min F = max S = δ⟨Ĥ⟩=0."
→ `equilibrium_as_extremum` (new node) with 7-domain table.

### Cross-Volume: Physical Solution Selection (A2)
Opus: "Each volume reinvents the same regularization→uniqueness pattern."
→ `physical_solution_selection` (new node) covering 5 volumes.

### Cross-Volume: Legendre Transform (U-2, P2)
Gap analysis: "Identical math in 4 volumes."
→ `canonical_transformation` now has Legendre universal table.

### Cross-Volume: Equipartition Bridge
Gap analysis: "Normal modes → equipartition hidden connection."
→ `normal_mode_decomposition` now has "→Equipartition Bridge" section.

---

## IMPROVED — Better But Not Complete

### Vol.1 C5: Bertrand's Theorem
Before: "Bertrand is ASSERTED in the reasoning node."
After: Node now says "This is a THEOREM requiring proof (perturbation
analysis of Δφ around circular orbit)." But the proof is still not supplied.
Agents need the perturbation expansion, which is a mathematical derivation
(~1 page), not a reasoning template.

### Vol.1: Runge-Lenz Vector (C7, opus issue 5)
Before: No node mentions the explicit form A = p×M − mα r̂.
After: Still not present. `separation_of_variables` mentions "hidden
symmetries" conceptually, but no node gives the vector or its conservation
proof. This is a knowledge-content gap, not a reasoning gap.

### Vol.2 C14: Noether Current for Fields
Before: T^{ik} is a memorized formula.
After: `constitutive_relation` cross-references the pattern but
doesn't give the field-theoretic Noether procedure: δL → ∂_k(ε^k L) →
T^{kl} = ∂L/∂(∂_k A_i)·∂^l A_i − g^{kl}L. This is a gap in the
Noether coverage — our symmetry_to_conservation only covers point mechanics.

### Vol.3: Spin / Ladder Operators (C13-14, V3-1 P1)
Before: Angular momentum node has eigenvalues but not the algebra.
After: Still not addressed. `knowledge.quantum.angular_momentum` gives
results but no reasoning node shows the ladder operator derivation:
[L_+, L_-]=2ℏL_z, eigenvalues l(l+1), half-integer from algebra alone.

### Vol.5/Vol.10: PT Quadruple Bridge (B-7, P2)
Before: 4 instances of PT in 4 volumes, no explicit parallel.
After: Individual nodes improved but no dedicated "universal PT structure"
node. The parallel between classical→quantum→statistical→many-body PT
remains implicit.

### Vol.6: Shock Entropy Condition (C1)
Before: Rankine-Hugoniot given but selection rule missing.
After: `physical_solution_selection` covers the PATTERN (regularization→
uniqueness) and explicitly lists shocks as an instance. But the specific
derivation of Δs≥0 from viscosity regularization is not given.

### Vol.8: ε(ω) Models (C1)
Before: "ε(ω) models are MODELS, not derivable from causality alone."
After: `linear_response_general` + `causality_to_analyticity` now make clear
that KK gives the GENERAL FRAMEWORK, while Drude/Lorentz are MODEL-SPECIFIC.
This is an important epistemological clarification — the agent now knows
the boundary between "universal" and "model-dependent."

---

## NOT ADDRESSED — Remaining Gaps

### P0: V4-2 Renormalization
"Biggest single gap in QED." Requires: regularization, counterterms,
running coupling, asymptotic freedom. None of our nodes cover this.
Needed: `reasoning.renormalization` — a major new node (~3-4 pages).

### P1: V6-1 Kolmogorov Turbulence
"30% of Vol.6 uncovered." Requires: inertial range, E(k)=C ε^{2/3} k^{-5/3},
Kolmogorov scale. Current coverage: zero.
Needed: `reasoning.turbulence_cascade` + `knowledge.fluid.kolmogorov`.

### P1: V5-1 Landau Theory of Phase Transitions
"Major Vol.5 topic." Requires: order parameter, F expansion, critical
exponents, Ginzburg criterion. Current coverage: zero.
Needed: `reasoning.phase_transition_landau`.

### P1: V3-1 Spin / Ladder Operators
"Needed for Vol.3 + Vol.5 magnetism." Requires: [L_+,L_-]=2ℏL_z,
eigenvalues l(l+1), half-integer spin, Pauli matrices.
Needed: `reasoning.angular_momentum_algebra`.

### P2: V4-1 Feynman Diagram Construction
"The leap from PT to Feynman diagrams requires a dedicated node."
Needed: `reasoning.feynman_diagram_construction`.

### Tier A: Cumulant Generating Function (A3)
"ln(generating functional) = connected sub-objects." Appears in
Vol.4 (connected diagrams), Vol.5 (cumulants), Vol.9 (linked-cluster).
Needed: `reasoning.cumulant_generating_function`.

### U-1: Field-Theoretic Noether
`symmetry_to_conservation` covers point mechanics. Field theory needs:
∂_k T^{kl} = 0 from translation invariance, Belinfante symmetrization.
Needed: expand existing node or create `reasoning.noether_field_theory`.

---

## OUT OF SCOPE — Mathematical Details

These are legitimate confusion points but are mathematical derivations
(not physics reasoning templates):

- Vol.1: Kepler algebra details, Liouville-Arnold theorem
- Vol.2: 4D δ-function integration, Airy/Bessel functions, pseudoscalar identity
- Vol.3: Distribution identity for sin²/α², Airy matching coefficients
- Vol.6: Boundary layer PDE solutions (Blasius, etc.)
- Vol.8: Crystal optics, anisotropic media Fresnel equation
- Vol.9: Bogoliubov transformation, BCS gap equation solution

These require mathematical facility, not improved reasoning templates.

---

## Priority for Round 2

If the user wants to continue improving, the highest-impact remaining gaps:

| Priority | Item | Impact |
|----------|------|--------|
| 1 | Field-theoretic Noether (U-1) | Bridges V1→V2 gap identified by 3 confusions |
| 2 | Spin/Ladder operators (V3-1) | Foundation for angular momentum across V3,V5 |
| 3 | Renormalization (V4-2) | Largest single gap in QED |
| 4 | Cumulant generating function (A3) | Unifies 3 volumes' diagrammatic methods |
| 5 | Phase transitions (V5-1) | Major Vol.5 topic uncovered |
