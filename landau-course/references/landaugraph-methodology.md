# LandauGraph — 3-Track Extraction Methodology

Proven workflow for distilling Landau volumes into the LandauGraph.
Repeated for Vol.1, 2, 5, 10 (55 nodes, 89 edges across 4 volumes).

## Workflow per Volume

### Phase 1: Read & Map

```
1. search.py to locate the book in KB
2. Read TOC and section headers (grep for '## §' and '# ')
3. Read key chapters — focus on sections that demonstrate reasoning patterns,
   not memorization of every equation. ~3-5 reading passes per volume is enough.
4. Identify: what is the CORE reasoning innovation of this volume?
   (Vol.1: variational → conservation. Vol.2: Lorentz → relativistic L.
    Vol.5: microcanonical → Gibbs distribution. Vol.10: Vlasov → Landau damping.)
```

### Phase 2: Track A — Reasoning Mining

**Goal**: Extract reusable physical thinking primitives.

**Prompt template**:
```
Read the text. Ignore chapter organization.
Extract reasoning skills — reusable physical thinking patterns.

Look for:
- Scale hierarchy / separation of scales
- Limiting cases and their validity conditions  
- Dominant balance arguments
- Symmetry → conservation chains
- Effective theory construction
- Instability criteria
- Variational logic
- Perturbation expansions and their convergence
- Dimensional analysis and scaling
- Adiabatic / quasistatic approximations

For each pattern: give it a skill_id, one-sentence trigger, and
identify the text passage that demonstrates it.
```

**Output**: 3-6 reasoning per volume. These become `reasoning.*.md` nodes.

### Phase 3: Track B — Knowledge Grounding

**Goal**: Attach concrete mechanisms to each reasoning pattern.

**Prompt template**:
```
For each reasoning skill from Track A, find ALL grounded physics mechanisms.
For each mechanism:
- Attach the key equation(s)
- Write the core physical picture (one sentence)
- List validity conditions
- Flag common misconceptions
- Note edge cases / failure modes
```

**Output**: 5-10 knowledge per volume. These become `knowledge.*.md` nodes.

### Phase 4: Track C — Dependency Mining

**Goal**: Establish prerequisite DAG + cross-volume analogies.

**Rules**:
- `prerequisite` edge: B cannot be understood without A
- `reasoning-instance` edge: B is a concrete realization of reasoning pattern A
- `analogy` edge: A and B share mathematical structure despite different physics
- `abstraction` edge: B is a more general formulation of A

**Cross-volume analogies are the highest-value edges.** Examples found:
- `multipole_expansion ↔ small_parameter_expansion` (a/λ ≪ 1 ↔ amp/eq ≪ 1)
- `adiabatic_invariance ↔ landau_damping` (both are timescale separation)
- `thermodynamic_perturbation ↔ small_parameter_expansion` (perturbation in different ensembles)
- `parametric_instability ↔ landau_damping` (mirror-symmetric: growth vs damping)

### Phase 5: Node Writing

Each node format:
```yaml
---
skill_id: reasoning.X or knowledge.X
type: reasoning | knowledge
summary_50t: >            # 50-token trigger-level summary
  ...
trigger:                  # When to load this node
  - ...
reasoning_role: ...       # For graph routing
parent: ...               # prerequisite parent
children: [...]           # prerequisite children
retrieval_cost: 1         # Load priority (1=cheap)
---

# Title

## Core Picture / Algorithm / Key Equations

## Edge Cases & Cross-References
```

### Phase 6: GRAPH.json Extension

Add nodes to `node_index`. Add edges to `edges[]`.
Update `meta.node_count`, `meta.edge_count`, `meta.volumes`.
Add rumination notes.

### Phase 7: Rumination (at volume boundaries)

After each volume, ask:
1. Are there hidden parent nodes? (e.g., `scale_separation` unifies 3 different reasoning nodes)
2. Are there duplicate concepts with different names?
3. What cross-volume analogies are now visible that weren't before?

## File Layout

```
/home/zhiping/.hermes/skills/landau-graph/
├── GRAPH.json                                    # 55 nodes, 89 edges
├── nodes/
│   ├── reasoning.variational_principle.md         # Vol.1 (10 reasoning)
│   ├── reasoning.symmetry_to_conservation.md
│   ├── ...
│   ├── reasoning.lorentz_invariance_to_action.md  # Vol.2 (6 reasoning)
│   ├── ...
│   ├── reasoning.ensemble_logic.md                # Vol.5 (4 reasoning)
│   ├── ...
│   ├── reasoning.kinetic_equation_closure.md      # Vol.10 (4 reasoning)
│   ├── ...
│   └── knowledge.*.md                            # 34 total knowledge nodes
```

## Pitfalls

- **Reading PDF instead of MD**: Always use `.md` from KB, never PDF.
- **Over-extraction**: Not every § is a reasoning pattern. Target 3-6 reasoning + 5-10 knowledge per volume.
- **Missing cross-volume analogies**: These are the most valuable edges. After each volume, re-scan ALL existing reasoning nodes for analogies.
- **Forgetting the edge weights**: 1.0 = essential prerequisite, 0.5-0.9 = strong connection, 0.1-0.4 = loose analogy.
