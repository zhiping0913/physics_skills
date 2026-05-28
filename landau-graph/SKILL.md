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

| Vol | Title | Nodes | Source |
|-----|-------|-------|--------|
| 1 | Mechanics | 21 | `~/knowledge_base/book/2004/2004--Механика/book.md` |
| 2 | Classical Fields | 14 | `~/knowledge_base/book/2003/2003--Классическая теория поля/book.md` |
| 3 | Quantum Mechanics | 7 | `~/knowledge_base/book/2002/2002--Квантовая механика (нерелятивистская теория)/book.md` |
| 4 | QED | 4 | `~/knowledge_base/book/2005/2005--Квантовая электродинамика/book.md` |
| 5 | Statistical Physics I | 11 | `~/knowledge_base/book/2002/2002--Статистическая физика. Часть 1/book.md` |
| 6 | Fluid Mechanics | 7 | `~/knowledge_base/book/2001/2001--Гидродинамика/book.md` |
| 7 | Elasticity | 2 | `~/knowledge_base/book/2003/2003--Теория упругости/book.md` |
| 8 | Electrodynamics of Continuous Media | 6 | `~/knowledge_base/book/2005/2005--Электродинамика сплошных сред/book.md` |
| 9 | Statistical Physics II | 5 | `~/knowledge_base/book/2001/2001--Статистическая физика. Часть 2/book.md` |
| 10 | Physical Kinetics | 10 | `~/knowledge_base/book/2002/2002--Физическая кинетика/book.md` |

All 10 volumes ruminated. All rewrite fixes applied. Source books are in the knowledge base as markdown (Russian originals).
