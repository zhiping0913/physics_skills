---
skill_id: knowledge.em.static_multipoles
type: knowledge
summary_50t: >
  Far from localized source: φ(r) = (1/4πε₀)[q/r + p·r̂/r² + ½Q_ij r̂_i r̂_j/r³ + ...].
  Monopole q = ∫ρ dV, dipole p = ∫r ρ dV, quadrupole Q_ij = ∫(3r_i r_j−r²δ_ij)ρ dV.
  Energy: U = qφ(0) − p·E(0) − ⅙Q_ij ∂_i E_j(0) + ...
trigger:
  - potential far from localized charge distribution
  - force/torque/energy of charge distribution in external field
reasoning_role: multipole_expansion_static
parent: reasoning.em.green_function_poisson
retrieval_cost: 1
---

# knowledge.em.static_multipoles

**Multipole expansion** of potential from localized ρ(r):

φ(r) = (1/4πε₀) Σ [q_lm Y_lm(θ,φ) / r^{l+1}]

**Cartesian moments** (Jackson §4.1):
- Monopole: q = ∫ ρ(r) dV
- Dipole: p = ∫ r ρ(r) dV
- Quadrupole: Q_ij = ∫ (3r_i r_j − r²δ_ij) ρ(r) dV  (traceless)
- Octupole, hexadecapole: higher-rank traceless tensors

**Energy in external field** (Jackson §4.6):
U = q φ(0) − p·E(0) − (1/6) Q_ij ∂_i E_j(0) + ...

**Force**: F = qE + ∇(p·E) + ...
**Torque**: N = p×E + ...

**Connection to spherical**: q_lm = √[4π/(2l+1)] ∫ r^l Y*_lm ρ dV.
The 2l+1 spherical components for each l correspond to the independent
components of the rank-l Cartesian tensor.

- Jackson §4.1-4.6
