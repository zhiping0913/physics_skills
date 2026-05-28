---
skill_id: reasoning.cumulant_generating_function
type: reasoning
summary_50t: >
  ln(generating functional) = sum of CONNECTED sub-objects only.
  Full expansion exponentiate: Z = exp(connected). The logarithm
  cancels disconnected diagrams/clusters. Unifies cumulants (V5),
  linked-cluster theorem (V9), and vacuum amplitude (V4).
trigger:
  - expanding a partition function or S-matrix
  - need connected (irreducible) correlations
  - canceling disconnected diagrams in perturbation theory
reasoning_role: connected_expansion
parent: reasoning.partition_to_thermodynamics
children:
  - knowledge.statistical.fluctuations
  - knowledge.condensed.diagram_technique
retrieval_cost: 1
---

# reasoning.cumulant_generating_function — ln Z = Connected Only

## Core Picture

A universal combinatorial fact appears in three different guises across
the Landau course:

```
FULL expansion (Z, S, generating functional)
    = exp( CONNECTED expansion )
    = 1 + connected + (connected)²/2! + (connected)³/3! + ...
```

The LOGARITHM strips away the exponentiation, leaving only connected
(irreducible) sub-objects. This single mathematical fact unifies:
- Statistical cumulants (Vol.5): ⟨E²⟩_c = ⟨E²⟩ − ⟨E⟩²
- Linked-cluster theorem (Vol.9): only connected diagrams contribute to G
- Vacuum amplitude cancellation (Vol.4): denominator cancels disconnected QED graphs

## The Pattern in Three Domains

### Statistical Mechanics (Vol.5 §15, §112)

The partition function Z = Σ exp(−E_n/T). Derivatives of ln Z give cumulants:
```
F = −T ln Z                              (free energy = extensive)
⟨E⟩ = −∂(ln Z)/∂β                        (first cumulant = mean)
⟨(ΔE)²⟩ = ∂²(ln Z)/∂β² = T² C_V         (second cumulant = variance)
⟨(ΔE)³⟩ = −∂³(ln Z)/∂β³                  (third cumulant = skewness)
```

**The crucial extensive-volume subtlety** (from Vol.5 rumination): Z itself
is ∝ exp(N), so ln Z = O(N) is extensive while Z is super-extensive.
The log cancels the volume divergence, leaving a well-behaved series.

### Quantum Many-Body Theory (Vol.9 §13)

The single-particle Green's function G is the sum of CONNECTED diagrams:
```
G(x,x') = sum of all connected Feynman diagrams
         = (full expansion) / (vacuum diagrams)
```
The denominator (vacuum amplitude) exactly cancels all disconnected
contributions to G. The linked-cluster theorem proves this rigorously.

### Quantum Field Theory (Vol.4 §72)

The S-matrix expansion: ⟨S⟩ = Σ(all diagrams). The vacuum amplitude ⟨0|S|0⟩
contains disconnected pieces. Physical amplitudes are:
```
⟨f|S|i⟩_physical = ⟨f|S|i⟩ / ⟨0|S|0⟩
```
The denominator cancels vacuum bubbles — exactly the same ln trick.

## Algorithm: From Full to Connected

```
1. Identify the generating object: Z (stat mech), ⟨S⟩ (QFT), G (many-body).
2. Write the formal expansion to all orders.
   The expansion contains BOTH connected and disconnected pieces.
3. Recognize: disconnected pieces are products of connected sub-pieces.
   Full expansion = Σ (products of connected pieces) = exp(connected).
4. Take ln: ln(full) = connected only.
5. Differentiate: n-th derivative of ln(full) at zero source = n-th cumulant.
```

## Why This Matters for Agents

Without this node, an agent encounters ln Z in Vol.5, ln S in Vol.4, and
connected diagrams in Vol.9 — and sees THREE DIFFERENT TRICKS. With this
node, they see ONE PATTERN applied in three domains.

## Cross-References

- Landau Vol.4 §72 (S-matrix expansion, vacuum amplitude)
- Landau Vol.5 §15, §112 (free energy, cumulants from ln Z)
- Landau Vol.9 §13 (linked-cluster theorem, connected diagrams)
- reasoning.partition_to_thermodynamics (parent: F = −T ln Z)
- reasoning.thermodynamic_perturbation_theory (related: ln Z cancellation)
- knowledge.statistical.fluctuations (⟨ΔE²⟩ = T²C_V from cumulants)
- knowledge.qed.feynman_rules (instance: vacuum amplitude cancellation)
