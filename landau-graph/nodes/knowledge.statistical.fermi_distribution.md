---
skill_id: knowledge.statistical.fermi_distribution
type: knowledge
summary_50t: >
  n̄_k = 1/[exp((ε_k−μ)/T)+1]. Fermi energy ε_F = μ(T=0).
  Degenerate at T ≪ ε_F: electrons fill states up to ε_F.
  Heat capacity C ∝ T (linear). Pauli paramagnetism.
trigger:
  - electrons in metals, white dwarfs
  - any fermionic many-body system
  - degenerate Fermi gas
reasoning_role: quantum_statistics_fermi
parent: reasoning.partition_to_thermodynamics
retrieval_cost: 1
---

# knowledge.statistical.fermi_distribution

**Fermi-Dirac**: n̄_k = 1/[exp((ε_k−μ)/T) + 1]

**Zero temperature**: n = 1 for ε < ε_F, n = 0 for ε > ε_F.
ε_F = (2πℏ)²(3π²n)^{2/3}/2m (non-relativistic).

**Degenerate electron gas** (T ≪ T_F = ε_F):
```
μ ≈ ε_F[1 − (π²/12)(T/ε_F)²]     chemical potential
E ≈ E_0 + (π²/6)g(ε_F)T²          energy
C_V ≈ (π²/3)g(ε_F)T               heat capacity ∝ T
```

**Magnetism** (Pauli): χ = (3/2)nμ_B²/ε_F (T-independent at low T).
Landau diamagnetism: χ_L = −(1/3)χ_P.

**Relativistic degenerate gas**: ε_F ≈ ℏc(3π²n)^{1/3} for n ≫ n_c.
Critical density: n_c = (mc/ℏ)³/3π².

- Landau Vol.5 §53-61
