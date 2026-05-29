# LandauGraph Extraction Methodology

Proven three-track workflow for distilling Landau-Lifshitz volumes into
reasoning-constrained skill graph nodes. Applied successfully to Volumes
1, 2, 3, 5, 6, 8, 10 (75 nodes, 125 edges across 7 volumes).

## Three-Track Extraction

### Track A — Reasoning Mining

**Goal**: Extract reusable physical thinking primitives. Ignore chapter
organization. Look for patterns, not just named concepts.

**Pattern categories to search for**:
- Scale hierarchy / separation of scales
- Limiting cases and their validity conditions
- Dominant balance arguments
- Symmetry → conservation / constraint chains
- Effective theory construction
- Instability criteria
- Variational logic
- Perturbation expansions and convergence conditions
- Dimensional analysis and scaling
- Adiabatic / quasistatic approximations
- Analytic continuation / pole prescriptions
- Generating function logic

**Output**: R-skills (reasoning primitives). These are the most reusable layer.
Each gets a `reasoning.*.md` node.

### Track B — Knowledge Grounding

**Goal**: For each reasoning skill from Track A, attach ALL concrete physics
mechanisms that instantiate it. Include equations, validity conditions,
physical pictures, worked examples, and edge cases.

**Output**: K-nodes (`knowledge.*.md`) connected to reasoning parents via
`reasoning-instance` edges.

### Track C — Dependency Mining

**Goal**: Establish the DAG of conceptual prerequisites. Which skills MUST
be understood before others? Ignore the textbook's exposition order — seek
conceptual dependency.

**Output**: `prerequisite` edges forming a directed acyclic graph.

## Node Format

Each node file contains YAML frontmatter (for graph search) + markdown body
(for context loading):

```yaml
---
skill_id: reasoning.variational_principle
type: reasoning
summary_50t: >            # ~50 tokens for graph scan
  All fundamental EOM follow from δS = 0. The Lagrangian is the system's
  fingerprint — find it, and dynamics are determined.
trigger:                  # when to load this skill
  - constructing equations of motion
  - new physical system without known EOM
reasoning_role: variational_logic
parent: null               # prerequisite parent
children: [...]            # dependent children
related: [...]             # analogy/abstraction links
retrieval_cost: 1
---
# Full skill body (~200-300 tokens)
## Core Picture
## Key Equations
## Assumptions
## Edge Cases
## Cross-References
```

## Edge Types

| Type | Meaning | Example |
|------|---------|---------|
| `prerequisite` | B requires A | `variational_principle` → `symmetry_to_conservation` |
| `reasoning-instance` | B is concrete realization of abstract pattern A | `scale_separation` → `dipole_approximation` |
| `abstraction` | B is more general form of A | `EM_wave` → `wave_equation_general` |
| `analogy` | A and B share identical math despite different physics | `landau_damping` ↔ `parametric_instability` |

## Rumination Process

After each volume extraction:
1. **Consolidation**: Merge duplicate skills, find hidden parent abstractions
2. **Compression**: Stress-test 50-token summaries — if a skill can't be compressed, split it
3. **Cross-volume**: Identify analogy edges between volumes (scale_separation in
   radiation ↔ small_parameter in mechanics ↔ adiabatic in invariants)

## Proven Volume Order

1. Vol.1 Mechanics — foundation (variational, symmetry, conservation, Hamilton)
2. Vol.2 Classical Fields — EM, relativity, radiation
3. Vol.5 Statistical Physics I — ensemble, Gibbs, partition function
4. Vol.10 Physical Kinetics — Boltzmann, Landau damping, plasma dielectric
5. Vol.8 Continuous Media — Kramers-Kronig, spatial dispersion
6. Vol.6 Fluid Mechanics — continuum limit, Navier-Stokes, similarity
7. Vol.3 Quantum Mechanics — Schrödinger, perturbation, WKB

Remaining: Vol.4 QED, Vol.7 Elasticity, Vol.9 Statistical Physics II.

## What NOT to extract

- Purely mathematical techniques without physical reasoning content
- Computational recipes (numerical integration methods, etc.)
- Material properties data (viscosity tables, dielectric constants)
- Sections that are 100% applications without new reasoning patterns
