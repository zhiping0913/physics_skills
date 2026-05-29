---
name: landau-distillation
description: "Distill physics textbooks into reasoning-constrained skill graphs. Three-track extraction (reasoning mining, knowledge grounding, dependency mining), three rumination types (consolidation, compression, paper feedback), four edge types."
---

# LandauGraph Distillation Methodology

## When to use

You are distilling a physics textbook (or any mathematically rigorous physical theory
text) into a graph of reasoning and knowledge nodes for AI agent consumption.

## Architecture

Three artifacts per node + one dynamic layer:
- **SKILL.md**: 50t YAML header + 300t body per node
- **GRAPH.json**: 4 edge types (prerequisite, reasoning-instance, analogy, abstraction)
- **KB pointer**: path to original text in knowledge base
- **LLM Wiki**: dynamic accumulation of domain applications (separate from static graph)

## Edge Types (4)

| Type | Meaning | Example |
|------|---------|---------|
| `prerequisite` | B cannot be understood without A | multipole → dipole |
| `reasoning-instance` | B is a concrete realization of A | scale_separation → WKB |
| `abstraction` | B is a more general form of A | EM_wave → wave_equation |
| `analogy` | A and B share mathematical structure | electrostatics ↔ magnetostatics |

## Extraction Workflow (per volume)

```
1. Read TOC + key sections from knowledge base (always .md, never .pdf)
2. Track A: Reasoning Mining
   → Extract reusable PHYSICAL THINKING PATTERNS (not just named entities)
   → Look for: scale hierarchy, limiting cases, dominant balance, symmetry,
     conservation, effective theory, instability, variational logic, perturbation
3. Track B: Knowledge Grounding
   → For each reasoning skill, attach: equations, physical pictures, validity,
     examples, misconceptions, edge cases
4. Track C: Dependency Mining
   → What MUST be known before what? Not textbook order — conceptual order.
   → Build prerequisite DAG
5. Write SKILL.md nodes (50t YAML header + 300t body)
6. Write GRAPH.json edges
7. Cross-volume pruning: add analogy/abstraction edges TO existing volumes
```

## Rumination Cycle (3 types)

### R1: Graph Consolidation
After each volume or periodically. Merge duplicate skills. Find hidden parent skills.
When 3+ skills share a reasoning pattern → create abstract parent.

### R2: Compression Pressure
Assume context budget = 200 tokens. Compress each skill. Preserve: trigger, picture,
equations. If compression fails → rewrite or split.

### R3: Paper Feedback
During agent use. If invoked skills successfully explain physics → strengthen edges.
If frequently invoked but useless → weaken. Discover new edges from usage.

## Node Format

```yaml
---
skill_id: domain.hierarchy.name
type: reasoning | knowledge
summary_50t: >
  One sentence — core picture + trigger conditions.
trigger:
  - condition 1
  - condition 2
reasoning_role: short_tag
parent: parent_skill_id
retrieval_cost: 1
---

# skill_id — Full Name

## Core Picture
[One paragraph: what is this, why it works, when to use it]

## Key Equations / Algorithm
[Numbered steps or key formulas with physical interpretation]

## Edge Cases & Failure Modes
[When this breaks, what the template misses]

## Cross-References
[KB path to original, other volumes, wiki pages]
```

## Critical Rules

1. **Never dump the textbook** — distill reasoning patterns, not chapter summaries.
2. **Equations with physical interpretation** — not just symbols. Say what each term MEANS.
3. **Edge cases are mandatory** — every reasoning node MUST say when it fails.
4. **Cross-volume connections matter** — analogy edges across volumes are Landau's hallmark.
5. **Knowledge base as fallback, not primary** — graph must be sufficient for 90% of queries.
6. **50t/300t discipline** — the agent scans headers; body is loaded on demand.

## Rumination Reports

- [Volume 1 Rumination](references/rumination-vol1.md) — 12 issues found, 2 hidden parent nodes identified.
