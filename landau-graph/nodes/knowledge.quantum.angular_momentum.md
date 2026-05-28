---
skill_id: knowledge.quantum.angular_momentum
type: knowledge
summary_50t: >
  [L_i,L_j] = iℏ ε_{ijk} L_k. L²|l,m⟩ = ℏ²l(l+1)|l,m⟩, L_z|l,m⟩ = ℏm|l,m⟩.
  l = 0,1,2,..., m = −l,...,l. Spin: s = ½,1,... Pauli matrices.
trigger:
  - quantum rotation, angular momentum
  - addition of angular momenta
  - spin, Pauli principle
reasoning_role: quantum_rotation
parent: knowledge.quantum.schrodinger_equation
retrieval_cost: 1
---

# knowledge.quantum.angular_momentum

**Commutation**: [L_i, L_j] = iℏ ε_{ijk} L_k. [L², L_z] = 0.

**Eigenvalues**: L²|l,m⟩ = ℏ² l(l+1) |l,m⟩, L_z|l,m⟩ = ℏm |l,m⟩.
l = 0, 1/2, 1, 3/2, ... ; m = −l, ..., +l. (2l+1)-fold degeneracy.

**Orbital** (integer l): L = r×p. Wave functions = spherical harmonics Y_lm.
Parity: P = (−1)^l.

**Spin** (§54-55): Intrinsic angular momentum. s = ½ for electron.
Spin operators: ŝ = (ℏ/2)σ. Pauli matrices:
σ_x = [[0,1],[1,0]], σ_y = [[0,−i],[i,0]], σ_z = [[1,0],[0,−1]].
Spinors: 2-component wave functions for s=½.

**Addition** (§31): J = L + S. |l−s| ≤ j ≤ l+s.
Clebsch-Gordan coefficients couple bases.

**Connection to classical**: Vol.1 §9 angular momentum conservation →
Vol.3 same commutation structure. Classical Poisson bracket {L_i,L_j}=ε_{ijk}L_k
maps to quantum commutator.

- Landau Vol.3 §26-31, §54-58
