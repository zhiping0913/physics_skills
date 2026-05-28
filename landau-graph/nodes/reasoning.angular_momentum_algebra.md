---
skill_id: reasoning.angular_momentum_algebra
type: reasoning
summary_50t: >
  From [J_i, J_j] = iℏε_{ijk} J_k alone: ladder operators J_± → eigenvalues
  ℏ²j(j+1). Half-integer j allowed by algebra but forbidden for orbital L=r×p.
  This defines spin. Pauli matrices σ_i for j=½.
trigger:
  - deriving angular momentum eigenvalues from commutation relations
  - understanding why spin must exist (half-integer from algebra)
  - constructing representations of SO(3)/SU(2)
reasoning_role: angular_momentum_quantum
parent: reasoning.classical_to_quantum_correspondence
children:
  - knowledge.quantum.angular_momentum
retrieval_cost: 1
---

# reasoning.angular_momentum_algebra — Commutator → Spectrum

## Core Picture

The classical angular momentum L = r × p becomes the operator L̂ = r̂ × p̂
with commutation relation [L̂_i, L̂_j] = iℏ ε_{ijk} L̂_k.

The crucial insight: this algebra ALONE determines the entire eigenvalue
spectrum, WITHOUT any reference to the orbital form r × p. The algebra
admits both integer AND half-integer eigenvalues. The half-integer ones
are FORBIDDEN for orbital angular momentum but ALLOWED for spin.

## Algorithm: From Commutators to Eigenvalues

**Step 1: Define L² and L_z.**
Since [L², L_z] = 0, they can be simultaneously diagonalized:
L²|λ,m⟩ = ℏ²λ|λ,m⟩,  L_z|λ,m⟩ = ℏm|λ,m⟩.

**Step 2: Construct ladder operators.**
L_± = L_x ± iL_y. Key commutators:
[L_z, L_±] = ±ℏ L_±        (L_± raises/lowers m by 1)
[L_+, L_-] = 2ℏ L_z        (measures the "spread")

**Step 3: Action on eigenstates.**
L_z(L_±|λ,m⟩) = ℏ(m±1)(L_±|λ,m⟩) → L_± changes m by ±1.

**Step 4: Bound m from above and below.**
L² − L_z² = ½(L_+L_- + L_-L_+) = L_+L_- − ℏL_z ≥ 0
→ ℏ²(λ − m² + m) ≥ 0 when applied to L_-|λ,m⟩
→ For maximum m = l: L_+|λ,l⟩ = 0 → λ = l(l+1)
→ For minimum m = −l: L_-|λ,−l⟩ = 0 → same λ

**Step 5: Count states.**
m runs from −l to +l in integer steps → 2l+1 values → l = 0, ½, 1, 3/2, 2, …

## Why Spin Exists

The algebra permits l = ½, 3/2, … But ORBITAL angular momentum L = r × p
has an additional property: e^{2πi L_z/ℏ} = 1 (single-valued wave function)
→ L_z eigenvalues must be integers → l must be integer.

**Therefore**: half-integer angular momentum CANNOT come from spatial motion.
It must be an INTRINSIC property — SPIN. The spin operator Ŝ satisfies the
SAME commutation relations [Ŝ_i, Ŝ_j] = iℏ ε_{ijk} Ŝ_k with NO orbital
representation.

## Spin-½ and Pauli Matrices

For s = ½ (the most important case):
ŝ = (ℏ/2)σ, where σ are the Pauli matrices:
σ_x = [[0,1],[1,0]], σ_y = [[0,-i],[i,0]], σ_z = [[1,0],[0,-1]]

Properties: σ_i σ_j = δ_{ij} + iε_{ijk} σ_k, Tr(σ_i) = 0, σ_i² = I.
Any 2×2 Hermitian matrix = a₀I + a·σ.

## Addition of Angular Momenta

Two angular momenta J₁ and J₂ combine: J = J₁ + J₂.
Total j runs from |j₁−j₂| to j₁+j₂ in integer steps.
Clebsch-Gordan coefficients give the explicit basis transformation.

## Cross-References

- Landau Vol.3 §27 (angular momentum in QM), §54 (spin)
- Landau Vol.4 §18 (Dirac spinors, spin-½)
- knowledge.quantum.angular_momentum (eigenvalues and CG coefficients)
- reasoning.classical_to_quantum_correspondence (parent: {,} → [,]/iℏ)
- reasoning.quantum_superposition (spin statistics: identical particles)
