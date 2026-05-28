---
skill_id: knowledge.mechanics.normal_modes
type: knowledge
summary_50t: >
  Near equilibrium, any coupled linear oscillator system is equivalent
  to s independent harmonic oscillators (normal modes) with frequencies
  ω_α from det|k_ij − ω²m_ij| = 0.
trigger:
  - coupled oscillators near equilibrium
  - small vibrations of molecules or lattices
reasoning_role: eigenvalue_diagonalization
parent: reasoning.normal_mode_decomposition
retrieval_cost: 1
---

# knowledge.mechanics.normal_modes

**Key equation**:
```
L = ½ Σ (m_ij ẋᵢẋⱼ − k_ij xᵢxⱼ)
→ Σ (−ω² m_ij + k_ij) Aⱼ = 0
→ det|k − ω²m| = 0 → s roots ω_α² > 0
→ Θ_α normal coordinates: θ̈_α + ω_α²Θ_α = 0
```

**Property**: Both T and U diagonalize simultaneously.
ω_α² guaranteed positive for stable equilibrium (m,k positive definite).

**Degeneracy**: Repeated roots → modes not uniquely defined.
Must use symmetry to fix.

- Landau Vol.1 §23-24
