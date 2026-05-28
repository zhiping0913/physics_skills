---
skill_id: reasoning.partition_to_thermodynamics
type: reasoning
summary_50t: >
  Z = Σ exp(−E_n/T). F = −T ln Z. All thermodynamic quantities follow
  from derivatives: S = −∂F/∂T, P = −∂F/∂V, E = F + TS.
  The partition function IS the theory.
trigger:
  - computing thermodynamic quantities from microscopic model
  - need free energy, entropy, pressure, heat capacity
  - any equilibrium statistical mechanics problem
reasoning_role: generating_function
parent: reasoning.microcanonical_to_canonical
children:
  - knowledge.statistical.free_energy
retrieval_cost: 1
---

# reasoning.partition_to_thermodynamics — Partition Function → All Thermodynamics

## Core Picture

Once you have Z(T,V,N) = Σ exp(−E_n/T), everything follows:
```
F = −T ln Z
S = −∂F/∂T      entropy
P = −∂F/∂V      pressure
E = F + TS      internal energy
C_V = T ∂S/∂T   heat capacity
```

This is the statistical physics analog of "find the Lagrangian and everything
follows." The partition function is the generating function for thermodynamics.

## Algorithm

```
1. Identify energy levels E_n(V,N) of the system
2. Compute Z = Σ_n exp(−E_n/T)  (sum over states, NOT levels — include degeneracy)
3. F = −T ln Z
4. All other quantities by differentiation
5. Check: F is extensive (F ∝ N) → requires correct counting of states
```

## Key Insight: F as Minimum Principle

For a system at fixed T, V: the equilibrium state MINIMIZES F.
This is the statistical analog of the mechanical minimum action principle.
When constraints are removed, the system evolves to the state of minimal F,
consistent with those constraints.

## The Classical Limit

Z_class = (1/N!h^{3N}) ∫ exp(−E(p,q)/T) d^{3N}p d^{3N}q
The factor 1/N! corrects for identical particle indistinguishability.
The factor 1/h^{3N} makes Z dimensionless (quantum origin, survives classical limit).

## Edge Cases

- **Degenerate energy levels**: Z = Σ g_n exp(−E_n/T), g_n = degeneracy
- **Continuous spectrum**: Z = ∫ ρ(E) exp(−E/T) dE
- **Grand canonical**: Ξ = Σ exp[(μN − E_nN)/T], Ω = −T ln Ξ

## Cross-References
- Landau Vol.5 §31 (free energy in Gibbs distribution)
- Landau Vol.5 §32 (thermodynamic perturbation theory)
- Landau Vol.1 §2: same role as Lagrangian — one function determines everything
