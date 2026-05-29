# Extraction Workflow — Three-Track Pipeline

## Prerequisites

- Source text in machine-readable format (markdown preferred)
- Knowledge base path for original reference
- Understanding of the discipline's domain structure

## Track A — Reasoning Mining

**Goal**: Extract REUSABLE PHYSICAL THINKING PATTERNS. Not chapter summaries.
Not named entities. The cognitive moves that transfer across problems.

### What to Look For

| Pattern | Signature | Example (Landau) |
|---------|-----------|-----------------|
| Scale hierarchy | Two or more disparate scales → separation | Fast/slow timescale → adiabatic invariant (V1) |
| Symmetry → conservation | Continuous symmetry of action → conserved current | Time translation → energy (V1), U(1) → charge (V2) |
| Effective theory | Integrate out fast/high-energy degrees | Effective potential from angular momentum (V1) |
| Variational logic | Equilibrium = extremum of functional | δS=0 (V1), min F (V5), δ⟨Ĥ⟩=0 (V3) |
| Perturbation expansion | Small parameter λ → series in λ | Mechanical (V1), quantum (V3), statistical (V5), many-body (V9) |
| Causality constraint | Response cannot precede cause → analyticity | Retarded GF (V2), Kramers-Kronig (V8), Landau iε (V10) |
| Dimensional analysis | Few parameters → dimensionless combinations → universal | Reynolds number (V6), Kolmogorov spectrum (V6) |
| Instability threshold | Parameter crosses critical value → new behavior | Parametric resonance (V1), turbulence onset (V6) |
| Physical solution selection | Multiple math solutions → regularization → unique | Retarded vs advanced (V2), shock entropy (V6), KK (V8) |
| Normal mode decomposition | Coupled linear system → independent oscillators | Small oscillations (V1), MHD waves (V6), plasma waves (V10) |

### Methodology

1. Read the original text section by section.
2. For each section, ask: "What is the PHYSICAL REASONING here?"
3. If the answer is a generic pattern (not tied to this specific system),
   extract it as a reasoning node.
4. Write: Core Picture (1 paragraph), Algorithm (numbered steps),
   Edge Cases (when it fails), Cross-References.

## Track B — Knowledge Grounding

**Goal**: For each reasoning pattern, attach the concrete physics that
instantiates it. These become knowledge nodes.

### What to Attach

- Key equation(s) with physical interpretation of every term
- Core physical picture (what's actually happening)
- Validity conditions (when does this apply?)
- Numerical/experimental benchmarks
- Edge cases and failure modes
- Landau section references

### Node Format

```yaml
---
skill_id: knowledge.domain.specific_topic
type: knowledge
summary_50t: >        # ~50 tokens for graph search
  ...
trigger:              # when to load this knowledge
  - condition 1
parent: reasoning.xxx # which reasoning pattern this instantiates
retrieval_cost: 1
---
```

## Track C — Dependency Mining

**Goal**: Build a directed acyclic graph (DAG) of prerequisites.

### Rules

1. **Conceptual order, not textbook order.** Landau puts electrostatics before
   magnetostatics for pedagogical reasons, but they're conceptually independent.
2. **If B uses a concept from A as a BLACK BOX, A → B is a prerequisite edge.**
3. **If B is a specialization of reasoning pattern A, A → B is a
   reasoning-instance edge.**
4. **If A and B share mathematical structure across domains, A ↔ B is an
   analogy edge.**

### Edge Types

| Type | Meaning | Direction |
|------|---------|-----------|
| `prerequisite` | B cannot be understood without A | A → B |
| `reasoning-instance` | B is a concrete realization of pattern A | reasoning → knowledge |
| `abstraction` | B is a more general formulation of A | specific → general |
| `analogy` | A and B share mathematical structure | A ↔ B (bidirectional) |

### Cross-Volume Bridges

After each volume, scan ALL previous volumes for analogy candidates.
The most powerful reasoning nodes are those that connect patterns
across seemingly unrelated domains. Examples from Landau:

- `constitutive_relation_from_symmetry`: viscous stress (V6) ↔ Hooke's law (V7) ↔ dielectric tensor (V8)
- `causality_to_analyticity`: ε(ω) (V8) ↔ generalized susceptibility (V5) ↔ plasma ε(k,ω) (V10)
- `cumulant_generating_function`: ln Z cumulants (V5) ↔ connected diagrams (V9) ↔ vacuum amplitude (V4)
