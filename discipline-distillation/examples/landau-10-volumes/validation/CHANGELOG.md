# LandauGraph Improvement Report — 2026-05-28

## Summary

Driven by blind-derivation experiment feedback from two independent agents
(DeepSeek V4 Flash + Claude Opus 4.7) across all 10 volumes. The agents
attempted to derive Landau's conclusions using only reasoning templates,
then reported every point where they got stuck.

**Net change: 89→96 nodes, 152→188 edges (+7 nodes, +36 edges)**

## Phase 1: Existing Node Improvements (10 nodes)

Modified existing reasoning nodes based on the most frequent agent complaints:
"templates give conclusions but not the constructive algorithm."

| Node | Key Addition |
|------|-------------|
| `variational_principle` | Full 7-step Galilean→L=½mv² construction algorithm (§4-§5) |
| `symmetry_to_conservation` | Hidden Dependencies: P formula needs L form, E=T+U needs T quadratic |
| `canonical_transformation` | Legendre Transform cross-volume universal table (V1→V5→V7→V8→V4) |
| `normal_mode_decomposition` | →Equipartition bridge (Dulong-Petit, quantum generalization) |
| `conservation_to_effective_reduction` | Bertrand theorem: assertion → theorem requiring proof |
| `classical_to_quantum_correspondence` | Epistemological shift: derivation (V1-2) → postulation (V3) |
| `constitutive_relation_from_symmetry` | Cross-volume trinity: viscous+Hooke+dielectric+conductivity |
| `causality_to_analyticity` | Promoted to general linear response entry point (7 susceptibility types) |
| `retarded_green_function` | LW potentials→fields: κ denominator, 1/R² vs 1/R decomposition |
| `quantum_superposition` | Identical particles: ±exchange → Pauli → Slater → Bose/Fermi |

## Phase 2: New Reasoning Nodes (7 nodes)

Created new nodes for cross-volume patterns that agents independently
discovered but had no template for.

| Node | Volumes | Core Pattern |
|------|---------|-------------|
| `physical_solution_selection` | V2,V5,V6,V8,V10 | Regularization→uniqueness: retarded waves, shock entropy, KK, Landau iε |
| `equilibrium_as_extremum` | V1,V2,V3,V5,V6,V7 | δS=0=min F=max S=δ⟨Ĥ⟩=0=min∫F dV (+ phase transitions) |
| `linear_response_general` | V5,V8,V9,V10 | χ(ω) analytic UHP→KK→FDT for ALL susceptibilities |
| `noether_field_theory` | V2,V4,V6,V7,V8 | Field symmetry→conserved current, T^{μν} from translation |
| `angular_momentum_algebra` | V3,V4 | [L_+,L_-]=2ℏL_z→l(l+1)→half-integer spin must exist |
| `cumulant_generating_function` | V4,V5,V9 | ln(generating functional)=connected sub-objects only |
| `renormalization` | V4 | UV divergence→regularization→counterterms→running coupling |

## Phase 3: Node Expansions (4 nodes)

| Node | Addition |
|------|----------|
| `separation_of_variables` | Runge-Lenz vector A=p×M−mαr̂, SO(4) hidden symmetry |
| `small_parameter_expansion` | PT quadruple bridge table (classical/quantum/statistical/many-body) |
| `dimensional_analysis_to_similarity` | Kolmogorov turbulence: v_λ∼(ελ)^{1/3}, k^{-5/3}, Richardson cascade |
| `green_function_method` | PT→Feynman diagrams bridge (Wick+Dyson+relativistic transition) |

## Phase 4: New Knowledge Nodes (2 nodes)

| Node | Content |
|------|---------|
| `knowledge.kinetic.vlasov_equation` | Vlasov equation, linearization, Landau's solution, analytic continuation |
| `knowledge.kinetic.plasma_instabilities` | Beam-plasma, two-stream, Weibel, ion-acoustic, Penrose criterion |

## Phase 5: Mathematics Theorems Skill

Created `mathematics-theorems` skill (accessible to all agents via `_global/`):
- `bertrand-theorem.md`: Complete proof that only U∝−1/r and U∝r² give closed orbits
- `liouville-arnold.md`: Integrability conditions, action-angle construction, failure modes

## Phase 6: Consistency Cleanup

- Removed 15 ghost children (frontmatter references to non-existent nodes)
- Removed 2 dangling edge references
- Added 5 missing parent edges
- Graph and disk now in perfect sync: 96=96 nodes, 0 dangling, 0 ghosts

## Verification

60+ agent confusions from the blind-derivation experiment were systematically
verified against improved nodes. All addressable gaps are closed. Remaining
mathematical details (Airy asymptotics, distribution limits, Bessel functions)
are out of scope for physics reasoning templates and belong in the
mathematics-theorems skill or specialized references.

## Agent-Reported Confusions: Resolution Summary

| Category | Count | Status |
|----------|-------|--------|
| Lagrangian construction (V1) | 4 | Resolved by variational_principle algorithm |
| Conservation law dependencies (V1) | 3 | Resolved by symmetry_to_conservation Hidden Dependencies |
| Field-theoretic T^{ik} (V2) | 3 | Resolved by noether_field_theory |
| Schrödinger epistemology (V3) | 2 | Resolved by classical_to_quantum epistemological shift |
| Spin algebra (V3) | 3 | Resolved by angular_momentum_algebra |
| Identical particles (V3,V5) | 2 | Resolved by quantum_superposition expansion |
| Legendre transform universality | 4 | Resolved by canonical_transformation table |
| Constitutive relation trinity | 3 | Resolved by constitutive_relation expansion |
| Linear response generality | 2 | Resolved by linear_response_general |
| PT quadruple bridge | 2 | Resolved by small_parameter_expansion table |
| Runge-Lenz hidden symmetry | 2 | Resolved by separation_of_variables expansion |
| Cumulant/ln-Z unity | 3 | Resolved by cumulant_generating_function |
| Renormalization logic | 1 | Resolved by renormalization |
| Physical solution selection | 5 | Resolved by physical_solution_selection |
| Kolmogorov turbulence | 1 | Resolved by dimensional_analysis expansion |
| Phase transitions | 1 | Resolved by equilibrium_as_extremum expansion |
| Feynman diagram construction | 1 | Resolved by green_function_method bridge |
| Mathematical theorems | 5 | Resolved by mathematics-theorems skill |
| LW field construction (V2) | 1 | Resolved by retarded_green_function expansion |
