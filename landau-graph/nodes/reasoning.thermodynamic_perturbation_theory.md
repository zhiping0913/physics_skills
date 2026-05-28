---
skill_id: reasoning.thermodynamic_perturbation_theory
type: reasoning
summary_50t: >
  H = H_0 + V. Free energy: F = F_0 + ⟨V⟩ − (1/2T)⟨(ΔV)²⟩ + ...
  Second-order correction ALWAYS negative. Condition: V/particle ≪ T.
  Wider convergence than quantum-mechanical perturbation theory.
trigger:
  - small correction to known system
  - weak interaction, weak external field
  - need thermodynamic quantities beyond ideal approximation
reasoning_role: perturbation_in_thermal_ensemble
parent: reasoning.partition_to_thermodynamics
retrieval_cost: 1
---

# reasoning.thermodynamic_perturbation_theory — Small Perturbation → Free Energy Shift

## Core Picture

Expand exp[−(H_0+V)/T] to second order in V. The result:
F = F_0 + ⟨V⟩ − (1/2T)⟨(V−⟨V⟩)²⟩

First order: mean value of perturbation energy.
Second order: ALWAYS negative — perturbation always lowers F.
This is the fluctuation-dissipation connection: the system adjusts
to exploit the perturbation, lowering free energy.

## Algorithm

```
1. Write H = H_0 + V, with V small compared to T (per particle)
2. Expand exp(−(H_0+V)/T) = exp(−H_0/T)[1 − V/T + V²/2T² + ...]
3. Compute Z = Z_0 · [1 − ⟨V⟩/T + ⟨V²⟩/2T² + ...]
4. F = −T ln Z = F_0 + ⟨V⟩ − (1/2T)⟨(V−⟨V⟩)²⟩
5. All averages taken with unperturbed distribution exp(−H_0/T)
```

## Quantum Case (§32)

Additional term from off-diagonal matrix elements:
F = F_0 + ⟨V_nn⟩ − ½ Σ_{nm}' |V_{nm}|²(w_m−w_n)/(E_n−E_m) − (1/2T)⟨(ΔV_nn)²⟩

All second-order terms are negative. Remarkably, this formula converges
even when the quantum-mechanical perturbation series for E_n diverges —
the thermal averaging improves convergence.

## Key Insight: Hidden Cancellation in ln Z

**Crucial subtlety** (Landau §32 footnote): When expanding exp(−V/T),
the ratio V/T is extensive (∝ N) — it is NOT small for macroscopic bodies.
The naive Taylor expansion appears invalid. However, the free energy
involves F = −T ln Z, and taking the LOGARITHM causes cancellation of
the large extensive terms, leaving a convergent series in the genuinely
small per-particle perturbation |V|/(NT) ≪ 1.

This is why thermodynamic perturbation theory works despite appearances:
the same cancellation occurs in all cumulant expansions (ln of a sum =
connected diagrams).

## Key Insight: Wider Convergence

Condition for thermodynamic PT: |V|/particle ≪ T.
Condition for quantum PT: |V| ≪ |E_n − E_m|.

These are DIFFERENT. At high T, thermodynamic PT may converge even when
quantum PT fails. At low T (T ≪ level spacing), the reverse may hold.

## Edge Cases

- **V is extensive**: Must use connected diagram expansion (Mayer cluster)
- **Degenerate ground state**: Perturbation must be treated in degenerate subspace
- **Low T**: Quantum PT may be needed instead of thermal PT

## Cross-References
- Landau Vol.5 §32 (thermodynamic perturbation theory)
- Landau Vol.3 §38 (quantum perturbation theory for energy levels)
- Landau Vol.9 §6: diagram technique for statistical physics
