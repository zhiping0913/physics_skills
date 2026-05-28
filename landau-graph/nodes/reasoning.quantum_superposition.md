---
skill_id: reasoning.quantum_superposition
type: reasoning
summary_50t: >
  Ψ = c₁Ψ₁ + c₂Ψ₂. Amplitudes ADD, not probabilities. |Ψ|²dq = probability.
  This is THE defining feature of quantum mechanics. Measurement collapses
  the superposition. Entanglement is superposition in composite systems.
trigger:
  - understanding quantum interference
  - two-slit experiment
  - any quantum system where classical intuition fails
reasoning_role: quantum_probability
parent: reasoning.classical_to_quantum_correspondence
children:
  - knowledge.quantum.wave_function
retrieval_cost: 1
---

# reasoning.quantum_superposition — Amplitudes Add, Not Probabilities

## Core Picture

In classical physics, probabilities of mutually exclusive events ADD:
P(A or B) = P(A) + P(B). In quantum mechanics, probability AMPLITUDES
add: Ψ = c₁Ψ₁ + c₂Ψ₂, and then P = |Ψ|² gives interference terms.

This is the mathematical expression of wave-particle duality. It is the
reason the double-slit experiment produces interference fringes rather
than the sum of single-slit patterns.

**The unique epistemological position of QM** (Landau §1): Quantum mechanics
contains classical mechanics as its limiting case (ℏ→0) AND simultaneously
requires classical mechanics for its own foundation — measurement
necessarily involves a classical apparatus. This circular dependence is
unprecedented among physical theories.

**Phase ambiguity** (Landau §2): The wave function is defined only up to
a global phase factor e^{iα}. This is a PRINCIPLED non-uniqueness — the
seed of U(1) gauge symmetry.

## The Measurement Problem

The wave function Ψ gives the probability of outcomes. But measurement
itself COLLAPSES the state: after measuring q and finding q₀, the state
becomes δ(q−q₀). The wave function is not the system — it is our
KNOWLEDGE of the system, encoded in a form that predicts measurement
statistics.

## Key Consequences

1. **Uncertainty principle** (§1, §16): Coordinate and momentum cannot
   simultaneously have definite values. ΔxΔp ≥ ℏ/2. This is a mathematical
   consequence of [x̂,p̂] = iℏ.

2. **Complete sets**: A set of simultaneously measurable quantities
   that fully specify the state (e.g., E, L², L_z for hydrogen).

3. **Density matrix** (§14): For incomplete knowledge, ρ̂ = Σ w_n|n⟩⟨n|.
   Pure state: ρ̂² = ρ̂. Mixed state: ρ̂² ≠ ρ̂, Tr ρ̂² < 1.

## Edge Cases

- **Continuous spectrum**: Normalization ∫|Ψ|² dq = 1 fails for plane waves
  and other continuous-spectrum states. Use δ-function normalization.
- **Phase ambiguity**: Ψ and Ψe^{iα} represent the SAME physical state.
  This is a principled non-uniqueness — all observables are bilinear in Ψ.
- **Identical particles** (Vol.3 §61-62): The superposition principle
  combined with indistinguishability forces a fundamental constraint:
  Ψ(1,2) = ±Ψ(2,1). The + sign (bosons) or − sign (fermions) is determined
  by spin (spin-statistics theorem). This leads to:
  * Pauli exclusion principle (fermions cannot occupy same state)
  * Slater determinants for fermion wave functions
  * Bose-Einstein and Fermi-Dirac statistics (Vol.5)
  * Exchange interaction energy: E_ex = ±⟨ψ₁ψ₂|V|ψ₂ψ₁⟩
  Without this, the entire edifice of multi-electron atoms, the periodic
  table, and quantum statistics has no foundation in the reasoning graph.

## Cross-References
- Landau Vol.3 §14 (density matrix)
- Landau Vol.1 §46 (Liouville → classical phase space density vs quantum density matrix)
