# LandauGraph — Methodology & Status

Date: 2026-05-25 | 84 nodes, 144 edges, 9/10 volumes

## Architecture

LandauGraph is a **Reasoning-Constrained Physics Skill Graph** inspired by Pipette
(https://skillgraph.pipette.bio/). Pipette's key insight: compile domain knowledge
into a graph prior that constrains the agent from arbitrary hallucination.

Physics version: edges encode REASONING dependencies, not workflow steps.

### Node Design (Two-Layer)

Each node is a SKILL.md with:
```
Layer 0 (50t header): skill_id, type, summary_50t, trigger, reasoning_role, parent, retrieval_cost
Layer 1 (300t body): Core Picture, Key Equations, Algorithm, Edge Cases, Cross-References
```

Layer 0 is loaded during graph search (scan many headers).
Layer 1 is loaded on retrieval (when a skill is selected).
Original Landau `.md` is consulted only when both layers are insufficient.

### 4 Edge Types

| Type | Meaning | Example |
|------|---------|---------|
| `prerequisite` | B requires A for understanding | multipole → dipole |
| `reasoning-instance` | B is a concrete realization of reasoning pattern A | scale_separation → dipole_approximation |
| `abstraction` | B is a more general formulation of A | EM_wave → wave_equation |
| `analogy` | Two domains share identical math structure | electrostatics ↔ elasticity |

Each edge carries a weight ∈ [0,1].

### 3-Track Extraction Pipeline

**Track A — Reasoning Mining**: Extract reusable physical thinking primitives
(scale hierarchy, symmetry→conservation, perturbation, adiabatic separation, etc.)

**Track B — Knowledge Grounding**: For each reasoning skill, find all concrete
physics mechanisms. Attach equations, physical pictures, validity conditions.

**Track C — Dependency Mining**: Establish conceptual DAG. Not "what does the
textbook present first" but "what MUST be understood first."

### 3 Rumination Types

1. **Graph Consolidation**: Merge duplicates, find hidden parent skills
   (e.g., adiabatic_invariance + Born-Oppenheimer → time_scale_separation)
2. **Compression Pressure**: Stress-test 50t and 300t summaries. If a skill
   cannot compress to <200 tokens preserving trigger+picture+equation+boundary,
   rewrite or split it.
3. **Paper Feedback Loop**: When agent reads papers and invokes skills, strengthen
   edges that help, weaken those that don't. The graph learns from usage.

### 3-Phase Retrieval Policy

1. **Domain Recognition** (~500t): Load top-level navigation skills for the domain
2. **Local Knowledge** (~1500t): Retrieve full bodies for 3-5 most relevant skills
3. **Reasoning Retrieval** (expensive, only on failure): Follow reasoning-instance
   edges upward to find abstract reasoning patterns

## Status: 9/10 Volumes Complete

### Graph Statistics
```
84 reasoning + knowledge nodes
144 typed edges
  prerequisite:       74
  reasoning-instance:  42  
  analogy:            24
  abstraction:          4
```

### Per-Volume Breakdown

| Vol | Domain | Reasoning | Knowledge | Total | Priority |
|-----|--------|-----------|-----------|-------|----------|
| 1 | Mechanics | 10 | 11 | 21 | Foundation |
| 2 | Classical Fields | 6 | 8 | 14 | Foundation |
| 3 | Quantum Mechanics | 4 | 3 | 7 | Foundation |
| 4 | QED | 2 | 2 | 4 | High |
| 5 | Statistical Physics I | 4 | 7 | 11 | High |
| 6 | Fluid Mechanics | 3 | 4 | 7 | Medium |
| 7 | Elasticity | — | — | — | PENDING |
| 8 | Continuous Media ED | 2 | 4 | 6 | Medium |
| 9 | Statistical Physics II | 3 | 2 | 5 | Medium |
| 10 | Physical Kinetics | 4 | 6 | 10 | Plasma-critical |

### Graph Trunk (5 Main Branches)

```
variational_principle (root)
├── [1] Mechanics: symmetry→conservation→Hamilton→Kepler
├── [2] EM/Relativity: Lorentz→gauge→Maxwell→Liénard-Wiechert→radiation
├── [5→9] Statistics: ensemble→Gibbs→Z→thermodynamics→Green's fns→Fermi liquid
├── [3→4] Quantum: correspondence→Schrödinger→WKB→Dirac→Feynman rules
└── [6→8→10] Continuum: Euler→Navier-Stokes→Kramers-Kronig→Landau damping
```

### Key Cross-Volume Bridges

| Bridge | Vol.1 | Vol.2/3/5/9/10 |
|--------|-------|-----------------|
| Adiabatic invariant → Bohr-Sommerfeld quantization | §49-52 | Vol.3 §48 (WKB) |
| Poisson bracket → commutator | §42 | Vol.3 (quantum) |
| Classical → Galilean-invariant L | §4 | Vol.2 §8 (Lorentz-invariant L) |
| Adiabatic invariant → magnetic moment | §49 | Vol.10 (μ = mv⊥²/2B) |
| Virial theorem (mechanics) | §10 | Vol.2 §34 (EM virial) |
| Liouville theorem | §46 | Vol.5 (ensemble logic) |
| Boltzmann H-theorem ← entropy | — | Vol.5→Vol.10 |
| Kernel circulation theorem ← Noether | §8 (classical) | continuous symmetry→conservation |

## File Locations

```
/home/zhiping/.hermes/skills/landau-graph/
├── GRAPH.json                    # 84 nodes, 144 edges, 4 edge types
├── nodes/
│   ├── reasoning.*.md            # 38 reasoning skill nodes
│   └── knowledge.*.md            # 46 knowledge nodes
│
/home/zhiping/task/
├── landau-skill-graph-plan.md    # Original master plan
├── lesson_pipette.md             # Design principles from Pipette
└── generate-landau-course.md     # Early design notes

/home/zhiping/knowledge_base/book/
├── 2001--Гидродинамика/          # Vol.6
├── 2001--Статистическая физика. Часть 2/  # Vol.9
├── 2002--Квантовая механика*/    # Vol.3
├── 2002--Статистическая физика. Часть 1/ # Vol.5
├── 2002--Физическая кинетика/    # Vol.10
├── 2003--Классическая теория поля/ # Vol.2
├── 2003--Теория упругости/       # Vol.7 (NOT YET DISTILLED)
├── 2004--Механика/               # Vol.1
├── 2005--Квантовая электродинамика/ # Vol.4
└── 2005--Электродинамика сплошных сред/ # Vol.8
```

## Volume Distillation Recipe

For each volume:
1. `search.py --title "..." --scope book` → locate KB directory
2. Read TOC + section headers → map chapter structure
3. Read key sections (focus on reasoning, not exhaustive reading)
4. Write reasoning nodes (transferable patterns: Trigger, Inputs, Algorithm, Edge Cases)
5. Write knowledge nodes (specific mechanisms: Key Equations, Assumptions, Validity)
6. Extend GRAPH.json with new nodes + edges (including cross-volume)
7. Update rumination notes

## Remaining Work

- Vol.7 (Теория упругости) — lowest priority; least connected to plasma physics
- Run Rumination 2 (compression pressure test) on all 84 nodes
- Enable Rumination 3 (paper feedback loop) once agents actively use the graph
