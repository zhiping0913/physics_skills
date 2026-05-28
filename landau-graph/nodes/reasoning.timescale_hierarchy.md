---
skill_id: reasoning.timescale_hierarchy
type: reasoning
summary_50t: >
  When a system has well-separated fast and slow dynamics, the fast
  motion can be averaged out, yielding an effective description.
  Adiabatic invariant + small-parameter expansion share this premise.
trigger:
  - system with multiple timescales (τ_fast ≪ τ_slow)
  - need to simplify by averaging over fast motion
  - conserved quantity emerges from slow variation
reasoning_role: timescale_separation
parent: reasoning.variational_principle
children:
  - reasoning.adiabatic_invariance
  - reasoning.small_parameter_expansion
related:
  - reasoning.multipole_expansion_radiation
retrieval_cost: 1
---

# reasoning.timescale_hierarchy — Separate Timescales → Effective Description

## Core Picture

When a system has two distinct timescales (τ_fast ≪ τ_slow), the fast
motion can be averaged over to produce a simpler effective description
of the slow dynamics. This is NOT a single template — it's a PREMISE
shared by multiple reasoning patterns:

- **Adiabatic invariance** (Vol.1): fast = orbital period T, slow = λ̇/λ
- **Small parameter expansion** (Vol.1): fast = linear oscillation, slow = nonlinear corrections
- **Multipole expansion** (Vol.2): fast = light crossing time a/c, slow = wave period T=2π/ω

All three extract simplified dynamics from the timescale hierarchy.

## When This Premise Holds

1. The timescales must be genuinely separated (τ_fast/τ_slow ≪ 1)
2. The fast motion must be bounded (periodic or quasiperiodic)
3. No resonances between fast and slow degrees of freedom

## When It Fails

- τ_fast ~ τ_slow: no separation to exploit
- Chaos: no well-defined fast/slow split
- Resonance crossing: fast and slow degrees exchange energy

## Cross-References
- reasoning.adiabatic_invariance (Vol.1 §49-52)
- reasoning.small_parameter_expansion (Vol.1 §21-24)
- reasoning.multipole_expansion_radiation (Vol.2 §66-67)
