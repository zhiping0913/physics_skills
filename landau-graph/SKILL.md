---
name: landau-graph
description: "LandauGraph — reasoning-constrained skill graph distilled from Landau-Lifshitz 10-volume Course of Theoretical Physics. 89 nodes, 152 edges. 4 edge types: prerequisite, reasoning-instance, abstraction, analogy. Provides retrieval access to reasoning templates and knowledge nodes for physics reasoning."
---

# LandauGraph — Landau-Lifshitz Reasoning Graph

A reasoning-constrained skill graph distilled from the complete 10-volume
Landau-Lifshitz Course of Theoretical Physics.

## Graph Structure

- **89 nodes**: ~30 reasoning templates + ~56 knowledge nodes
- **152 edges**: prerequisite (79), reasoning-instance (43), analogy (26), abstraction (4)
- **3 hidden parent nodes**: symmetry_drives_physics, timescale_hierarchy, causality_as_constraint
- **4 edge types**: prerequisite, reasoning-instance, abstraction, analogy

## File Layout

```
landau-graph/
├── SKILL.md            # This file
├── GRAPH.json          # Full graph topology (nodes + edges)
├── nodes/              # Individual node .md files
│   ├── reasoning.*.md  # Reasoning templates (algorithm + edge cases)
│   └── knowledge.*.md  # Knowledge nodes (formulas + facts)
└── rumination/         # Per-volume rumination reports and fix logs
    ├── vol{N}.md       # Rumination report for volume N
    └── vol{N}-rewrite-fixes.md  # Applied content fixes
```

## How to Use

### Retrieval

Load `GRAPH.json` to get the full topology. For each node, read
`nodes/{node_id}.md` for the complete content (Core Picture, Algorithm,
Edge Cases, Cross-References).

### Node Types

- **reasoning.*.md**: Reasoning templates with trigger conditions, algorithms,
  edge cases, and cross-references. Designed for agent retrieval.
- **knowledge.*.md**: Reference knowledge — formulas, definitions, parameter
  ranges. Anchored to Landau sections.

### Edge Types

- **prerequisite**: Node B requires Node A (logical dependency)
- **reasoning-instance**: Knowledge node is a concrete instance of a reasoning pattern
- **abstraction**: Node abstracts a pattern from multiple instances
- **analogy**: Non-identical but structurally similar reasoning

### Volume Coverage

| Vol | Title | Nodes | Status |
|-----|-------|-------|--------|
| 1 | Mechanics | 21 | Rumin. ✓ |
| 2 | Classical Fields | 14 | Rumin. ✓ |
| 3 | Quantum Mechanics | 7 | Rumin. ✓ |
| 4 | QED | 4 | Rumin. ✓ |
| 5 | Statistical Physics I | 11 | Rumin. ✓ |
| 6 | Fluid Mechanics | 7 | Rumin. ✓ |
| 7 | Elasticity | 2 | Rumin. ✓ |
| 8 | Electrodynamics of Continuous Media | 6 | Rumin. ✓ |
| 9 | Statistical Physics II | 5 | Rumin. ✓ |
| 10 | Physical Kinetics | 10 | Rumin. ✓ |

All 10 volumes ruminated. All rewrite fixes applied.
