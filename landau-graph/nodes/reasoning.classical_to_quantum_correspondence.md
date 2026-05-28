---
skill_id: reasoning.classical_to_quantum_correspondence
type: reasoning
summary_50t: >
  Classical mechanics: H(p,q). Quantum: H → Ĥ = H(−iℏ∇, q). 
  Schrödinger: iℏ∂Ψ/∂t = ĤΨ. In ℏ→0 limit: Ψ ~ exp(iS/ℏ) → 
  S satisfies Hamilton-Jacobi. The bridge from classical to quantum.
trigger:
  - constructing quantum Hamiltonian from classical system
  - understanding classical limit of quantum mechanics
  - canonical quantization of any classical theory
reasoning_role: quantization_prescription
parent: reasoning.canonical_transformation
children:
  - knowledge.quantum.schrodinger_equation
  - knowledge.quantum.wkb_approximation
retrieval_cost: 1
---

# reasoning.classical_to_quantum_correspondence — Classical Mechanics → Quantum Operator Formalism

## Core Picture

The bridge from classical to quantum mechanics is the correspondence
principle: take the classical Hamiltonian H(p,q) and replace the
momentum p with the operator −iℏ∇. The resulting operator Ĥ generates
time evolution via the Schrödinger equation iℏ∂Ψ/∂t = ĤΨ.

This is NOT derived from classical mechanics — it is a NEW postulate.
But it guarantees that in the limit ℏ→0, quantum mechanics recovers
classical mechanics: Ψ = a·exp(iS/ℏ) → S satisfies the H-J equation.

**Epistemological shift from Vol.1-2**: In classical mechanics and field
theory, EVERYTHING followed from a single principle (δS = 0). The Schrödinger
equation cannot be derived this way — it requires NEW postulates:
(1) physical states are vectors in a Hilbert space,
(2) observables are Hermitian operators,
(3) the superposition principle → the equation must be LINEAR,
(4) [q̂,p̂] = iℏ (the fundamental commutation relation).
Landau's footnote (§17): "This statement is not a logical consequence of
the basic principles of quantum mechanics and should be regarded as a
consequence of experimental data." The correspondence p→−iℏ∇ is a
PRESCRIPTION, not a theorem. This is a fundamentally different
epistemological status from the derivations in Vol.1 and Vol.2.

## Algorithm

```
1. Write classical H(p,q) for the system
2. Replace p → −iℏ∇ (coordinate representation)
3. Schrödinger equation: iℏ ∂Ψ/∂t = ĤΨ
4. For stationary states: Ψ = ψ(q)e^{−iEt/ℏ} → Ĥψ = Eψ
5. ℏ→0 limit: Ψ = exp(iS/ℏ), substitute → S satisfies H-J eqn
```

## Why This Specific Correspondence

- **Galilean invariance**: H = p²/2m is the ONLY form consistent with
  homogeneity, isotropy, and Galilean relativity — same argument as
  classical (Vol.1 §4), applied to operators.
- **Potential energy is empirical**: The potential U(r₁,r₂,...) in Ĥ is
  NOT derived from quantization. Landau §17 footnote: "Это утверждение
  не является логическим следствием основных принципов квантовой
  механики и должно рассматриваться как следствие опытных данных."
  It is copied from classical mechanics by empirical correspondence.
- Linearity: the superposition principle (§2) REQUIRES the equation
  to be linear → Ĥ must be a linear operator.
- Self-adjointness: Ĥ = Ĥ† guarantees real eigenvalues (observable energies).

## The Deep Connection: Poisson Bracket → Commutator

Classical: {f,g} = Σ(∂f/∂q ∂g/∂p − ∂f/∂p ∂g/∂q).
Quantum: [f̂,ĝ] = iℏ{f,g}̂. The fundamental commutation relation
[x̂,p̂] = iℏ is the quantum version of {x,p} = 1.

## Cross-References
- Landau Vol.3 §17 (Schrödinger equation), §46 (WKB/quasiclassical)
- Landau Vol.1 §40 (Hamilton equations), §47 (H-J equation) — classical foundation
- Landau Vol.1 §42 (Poisson brackets → quantum commutators)
