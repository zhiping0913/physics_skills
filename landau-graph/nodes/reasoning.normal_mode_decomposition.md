---
skill_id: reasoning.normal_mode_decomposition
type: reasoning
summary_50t: >
  A coupled linear system is diagonalized by a coordinate transformation.
  The eigenvalues ω_α² are the squared normal frequencies.
  The system becomes s independent harmonic oscillators.
trigger:
  - coupled linear oscillators
  - need to find independent modes
  - analyzing eigenmodes of a physical system
reasoning_role: eigenvalue_diagonalization
parent: reasoning.small_parameter_expansion
children:
  - knowledge.mechanics.normal_modes
related:
  - reasoning.separation_of_variables
retrieval_cost: 1
---

# reasoning.normal_mode_decomposition — Coupled System → Independent Modes

## Core Picture

A system of s coupled linear oscillators looks complicated in arbitrary
coordinates, but there exists a SPECIAL coordinate system — normal
coordinates Θ_α — in which the equations completely decouple:
θ̈_α + ω_α² Θ_α = 0.

This is a simultaneous diagonalization of TWO quadratic forms (T and U),
not just one matrix. The requirement that both forms be positive definite
guarantees real, positive eigenvalues ω_α².

## Algorithm

```
1. Write T = (1/2) Σ m_ij ẋ_i ẋ_j,  U = (1/2) Σ k_ij x_i x_j
2. Assume harmonic time dependence: x_k = A_k e^{iωt}
3. Obtain algebraic eigenvalue problem: Σ (−ω²m_ij + k_ij) A_j = 0
4. Characteristic equation: det|k_ij − ω²m_ij| = 0  →  s roots ω_α²
5. For each ω_α, find eigenvector A_k^(α) from minors
6. Normal coordinates: Θ_α, each obeying θ̈_α + ω_α²Θ_α = 0
7. L = Σ (m_α/2)(θ̇_α² − ω_α²Θ_α²)
```

## Why ω² is Always Positive

From the eigenvalue equation:
ω² = (Σ k_ij A_i* A_j) / (Σ m_ij A_i* A_j)
Both quadratic forms are positive definite → ω² > 0.
The proof uses symmetry (k_ij = k_ji, m_ij = m_ji).

## Degeneracy

If characteristic equation has repeated roots → degenerate frequencies.
Any linear combination of the degenerate eigenvectors is also a normal mode.
Additional conditions (symmetry) may be needed to fully specify.

## Edge Cases

- **m_ij not positive definite**: e.g., one mass zero → singular,
  need constraint treatment
- **Zero frequency**: ω² = 0 mode → translational/rotational invariance
  of the whole system

## Cross-References

- Landau Vol.1 §23-24 (Small oscillations, forced oscillations)
- Landau Vol.6 §69 (MHD waves — normal modes in continuum)
- Landau Vol.10 §29 (Plasma oscillations — longitudinal normal mode)

## Cross-Volume Bridge: Normal Modes → Equipartition (Vol.5)

Each normal mode is an independent harmonic oscillator with energy
ε_α = ½ω_α²|Θ_α|² + ½|Θ̇_α|². In classical statistical mechanics (Vol.5),
the equipartition theorem assigns ½T to EACH quadratic degree of freedom →
each normal mode contributes T (not ½T!) because it has two quadratic terms
(kinetic + potential). This is the microscopic foundation of the
Dulong-Petit law (heat capacity = 3N for N atoms in a solid), and its
quantum generalization (Einstein/Debye models) comes from quantizing
each normal mode.

**Pattern**: Whenever a system decomposes into independent harmonic modes,
each mode contributes energy according to its statistics: classical = T,
quantum = ℏω/(e^{ℏω/T}−1). This applies to phonons, photons, magnons,
and plasma oscillations across Vol.5, Vol.9, and Vol.10.
- Quantum: same math → phonon modes in solids
- Plasma: electrostatic normal modes (Langmuir, ion-acoustic)
