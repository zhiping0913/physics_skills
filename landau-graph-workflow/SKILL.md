---
name: landau-graph-workflow
description: "Three-track extraction workflow for distilling Landau-Lifshitz volumes into the LandauGraph skill graph. Use when continuing distillation of remaining volumes."
---

# LandauGraph Distillation Workflow

Three-track extraction pipeline for turning Landau-Lifshitz volumes into
reasoning + knowledge SKILL.md nodes linked by a typed GRAPH.json.

## Prerequisites

- Knowledge base: `/home/zhiping/knowledge_base/book/`
- Graph root: `/home/zhiping/task/landau-graph/`
- Volumes completed: 1 (Mechanics), 2 (Fields), 5 (Stat.Phys.I), 8 (Continuous Media), 10 (Kinetics)

## Three-Track Extraction (per volume)

### Track A — Reasoning Mining

Read the entire volume's markdown from the knowledge base. Ignore chapter
organization. Extract **reusable physical thinking patterns**, NOT chapter summaries.

Look for:
- Scale hierarchy / separation of scales
- Limiting cases and their validity conditions
- Dominant balance arguments
- Symmetry → conservation chains
- Effective theory construction
- Instability criteria and thresholds
- Variational logic
- Perturbation expansions and convergence
- Dimensional analysis / scaling
- Adiabatic / quasistatic approximations
- Analytic continuation / causality constraints

Each reasoning pattern becomes a `reasoning.*` node.

### Track B — Knowledge Grounding

For each reasoning skill from Track A, find ALL concrete physics mechanisms
that instantiate it. Each becomes a `knowledge.*` node.

For each mechanism attach: key equation(s), core physical picture,
validity conditions, edge cases, and Landau section references.

### Track C — Dependency Mining

Identify which skills MUST be understood before others. Establish a DAG of
prerequisites. Ignore the textbook's exposition order — seek conceptual dependency.

## Node Format

Each node is a markdown file at `nodes/{skill_id}.md` with YAML frontmatter:
```yaml
---
skill_id: reasoning.causality_to_analyticity
type: reasoning          # reasoning | knowledge
summary_50t: >           # ~50 token summary for graph search
  ...
trigger:                 # when to apply this skill
  - condition 1
reasoning_role: ...      # category for search/routing
parent: ...              # prerequisite reasoning node
children: [...]          # dependent nodes
retrieval_cost: 1
---
```

The body follows with: Core Picture, Algorithm (for reasoning nodes),
Key Equations (for knowledge nodes), Edge Cases, Cross-References.

## Graph Format (GRAPH.json)

Single JSON file in the graph root. Contains:
- `node_index`: all nodes with file paths and metadata
- `edges`: typed connections between nodes

Four edge types:
- `prerequisite`: B cannot be understood without A
- `reasoning-instance`: B is a concrete realization of reasoning pattern A
- `abstraction`: B is a more general formulation of A
- `analogy`: A and B share mathematical structure across domains

Each edge carries a `weight` ∈ [0,1].

## Rumination (after each volume)

1. **Graph Consolidation**: Find hidden parent skills — when 3+ skills share
   a reasoning pattern, create the parent. Record in `rumination_1_notes`
   in GRAPH.json.

2. **Cross-volume edges**: For each new volume, identify analogy and
   abstraction edges connecting to previously distilled volumes.

## Volume Priority

1. Vol.2 (Fields) — foundation for all physics agents
2. Vol.5 (Stat.Phys.I) — prerequisite for Vol.10
3. Vol.10 (Kinetics) — plasma relevance, Landau damping
4. Vol.8 (Continuous Media) — dielectric theory, MHD
5. Vol.6 (Fluid Dynamics) — hydrodynamics, instabilities
6. Vol.3 (Quantum Mechanics)
7. Vol.4 (QED)
8. Vol.9 (Stat.Phys.II)
9. Vol.7 (Elasticity)

Volumes 1-5,8,10 completed. Vol.6 next.

## Pitfalls

- Reading only the primary `.md` file — always read ALL `.md`/`.txt` in the
  paper or book directory (supplemental materials carry key derivations).
- Chapter-summary mode: Landau's § structure is NOT the graph structure.
  One section may yield 3 skills; one skill may span 4 sections.
- Forgetting cross-volume edges: always scan existing reasoning nodes for
  analogy candidates when adding new nodes.
- Node file not referenced in GRAPH.json `node_index` — causes silent omission.
