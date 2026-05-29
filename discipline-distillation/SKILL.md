---
name: discipline-distillation
description: "Universal methodology for distilling any mathematically rigorous discipline into a reasoning-constrained skill graph consumable by AI agents. Three-track extraction (reasoning mining, knowledge grounding, dependency mining), systematic rumination with blind-derivation validation, and cross-volume bridge construction. Complete worked example: Landau-Lifshitz 10-volume Course of Theoretical Physics (96 nodes, 188 edges)."
---

# Discipline Distillation — From Textbook to Reasoning Graph

## What This Is

A complete, battle-tested methodology for turning a textbook (or any
mathematically rigorous body of knowledge) into a graph of reasoning
templates and knowledge nodes that AI agents can use for autonomous
physics reasoning — without access to the original text.

**Worked example**: Landau-Lifshitz 10-volume Course of Theoretical Physics
→ 96 reasoning + knowledge nodes, 188 typed edges, validated by two
independent AI agents in blind-derivation experiments.

## The Big Picture

```
TEXTBOOK(S)
    ↓ Track A: Extract reusable reasoning patterns
    ↓ Track B: Ground each pattern in concrete knowledge
    ↓ Track C: Map conceptual dependencies
REASONING GRAPH (nodes + typed edges)
    ↓ Rumination: re-read original, find hidden premises, fix
    ↓ Cross-volume: build bridges between volumes
    ↓ Validation: blind-derivation experiment
PRODUCTION GRAPH (agent-consumable)
```

## Three Phases

### Phase 1: Extraction

Three-track extraction per volume/section. Full details: `references/extraction-workflow.md`

- **Track A — Reasoning Mining**: Find reusable PHYSICAL THINKING PATTERNS
  (not chapter summaries). Scale hierarchy, symmetry→conservation, effective
  theory, variational logic, perturbation, causality constraints, dimensional
  analysis, adiabatic approximations.
- **Track B — Knowledge Grounding**: For each reasoning pattern, attach
  concrete physics: equations, physical pictures, validity conditions,
  edge cases, misconceptions.
- **Track C — Dependency Mining**: What MUST be known before what?
  Conceptual order, not textbook order. Build prerequisite DAG.

### Phase 2: Rumination

After extraction, systematically re-read the original text with the graph
loaded. Find hidden premises, missing edge cases, unstated assumptions.
Full details: `references/rumination-workflow.md`

Critical lesson from Landau distillation: **fast passes that find "no issues"
are diagnostically wrong.** Every volume (10/10) had issues when properly
re-read. Common patterns: `references/rumination-check-patterns.md`

### Phase 3: Validation

The acid test: give the reasoning graph (WITHOUT the original text) to
independent AI agents. Ask them to derive the discipline's core results.
Every point where they get stuck is a gap in the graph.

Full details: `references/blind-derivation-validation.md`

## Worked Example: Landau-Lifshitz 10 Volumes

See `examples/landau-10-volumes/` for the complete distillation record.

| Aspect | Result |
|--------|--------|
| Source | 10 volumes, ~7000 pages, Russian original |
| Output | 96 nodes (37 reasoning + 59 knowledge), 188 edges |
| Rumination | All 10 volumes ruminated, 80+ fixes applied |
| Hidden parents | 3 discovered (symmetry_drives_physics, timescale_hierarchy, causality_as_constraint) |
| Validation | 2 independent AI agents, 60+ confusions reported and resolved |
| Iterations | 3 rounds of blind-derivation → fix → re-validate |

## Skills Consolidated Here

This skill supersedes and replaces:
- `landau-distillation` (methodology)
- `landau-graph-workflow` (extraction pipeline)
- `landau-rumination` (rumination workflow + check patterns)

The `landau-graph` skill remains as the PRODUCTION GRAPH (96 nodes, 188 edges)
— it is the OUTPUT of this methodology applied to Landau.
