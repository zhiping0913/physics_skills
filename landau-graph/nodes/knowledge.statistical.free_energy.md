---
skill_id: knowledge.statistical.free_energy
type: knowledge
summary_50t: >
  F = −T ln Z. All thermodynamics from derivatives.
  F = E − TS. Minimized at equilibrium for fixed T,V.
  dF = −S dT − P dV + μ dN.
trigger:
  - computing thermodynamic potentials
  - equilibrium conditions
  - relating microscopic model to measurable quantities
reasoning_role: thermodynamic_potential
parent: reasoning.partition_to_thermodynamics
retrieval_cost: 1
---

# knowledge.statistical.free_energy

**Definition**: F = −T ln Z, Z = Σ exp(−E_n/T).

**Key relations**:
```
S = −∂F/∂T        P = −∂F/∂V        μ = ∂F/∂N
E = F + TS         C_V = −T ∂²F/∂T²
```

**Minimum principle**: At fixed T,V, equilibrium state minimizes F.
Removing a constraint → system evolves to new minimum of F.

**Thermodynamic identity**: dF = −S dT − P dV + μ dN.

**Perturbation**: F = F_0 + ⟨V⟩ − (1/2T)⟨(ΔV)²⟩ (see reasoning.thermodynamic_perturbation_theory).

**Grand potential**: Ω = −T ln Ξ = −PV (for homogeneous system).
Ξ = Σ exp[(μN − E_nN)/T].

- Landau Vol.5 §15, §31
