---
skill_id: reasoning.separation_of_variables
type: reasoning
summary_50t: >
  When the Hamilton-Jacobi equation can be split into independent
  pieces per coordinate, the system is integrable with s conserved
  quantities. Cyclic coordinates are the trivial case.
trigger:
  - attempting to integrate equations of motion
  - system appears integrable but not trivially solvable
  - need to find all constants of motion
reasoning_role: integrability_condition
parent: reasoning.canonical_transformation
children:
  - knowledge.mechanics.action_angle_variables
related:
  - reasoning.adiabatic_invariance
  - reasoning.normal_mode_decomposition
retrieval_cost: 1
---

# reasoning.separation_of_variables — Separate Coordinates → Complete Integrability

## Core Picture

The Hamilton-Jacobi equation ∂S/∂t + H(q, ∂S/∂q, t) = 0 is a PDE for S.
If the variables separate — meaning each coordinate q_i appears only in
combination with its own ∂S/∂q_i — then the PDE reduces to s independent
ODEs, each yielding one constant of motion.

This is the most powerful integration method in classical mechanics.
When it succeeds, the system is COMPLETELY INTEGRABLE.

## Algorithm

```
1. Write H-J equation: ∂S/∂t + H(q₁,...,q_s, ∂S/∂q₁,..., ∂S/∂q_s) = 0
2. For conservative systems: S = S₀(q) − Et, reducing to
   H(q, ∂S₀/∂q) = E
3. Seek separated solution: S₀ = Σ S_k(q_k)
4. If the equation contains φ(q₁, dS₁/dq₁) without any other q_i:
   φ(q₁, dS₁/dq₁) = α₁ (constant)
   → S₁ determined by quadrature
5. Repeat for each coordinate → s constants α₁,...,α_s
6. The final solution: S = Σ S_k(q_k; α₁,...,α_s) − E(α₁,...,α_s)t
```

## Cyclic Coordinates as Special Case

If q₁ doesn't appear in H → ∂S/∂q₁ appears alone → S₁ = α₁q₁.
The separation constant α₁ IS the conserved momentum p₁.

## When Separation is Possible

In spherical coordinates with U = a(r) + b(θ)/r² + c(φ)/r²sin²θ,
separation always succeeds.
In parabolic coordinates with U = [a(ξ)+b(η)]/(ξ+η), also separates.

The Kepler problem separates in BOTH spherical and parabolic coordinates
→ a signature of its hidden symmetry (Runge-Lenz vector).

## Edge Cases

- **Non-separable systems**: Most potentials do not separate.
  The system may still be integrable (e.g., Toda lattice) but H-J won't split.
- **Degeneracy**: When frequencies are commensurate, the number of
  independent frequencies is less than s.

## Hidden Symmetries and the Runge-Lenz Vector

Separability in MULTIPLE coordinate systems signals a hidden symmetry
beyond the obvious geometric ones. The Kepler problem separates in BOTH
spherical AND parabolic coordinates — this is NOT generic. It signals
an extra conserved quantity: the Runge-Lenz vector.

**For U = −α/r (Kepler problem)**:
```
A = p × M − mα r̂
```
where M = r × p is the angular momentum.

**Properties**:
- A is conserved (dA/dt = 0) — check by direct differentiation
- A lies in the orbit plane (A·M = 0)
- |A| = mαe where e is the eccentricity
- A points from the focus to the perihelion
- A² = m²α² + 2mE M² → relates energy to eccentricity

**Hidden SO(4) symmetry**: For E < 0 (bound orbits), the conserved
quantities M and A form an SO(4) algebra. Combined with the Hamiltonian,
this explains why ALL bound Kepler orbits close — the system has more
conserved quantities than degrees of freedom (superintegrability).

**Pattern**: When a system separates in more coordinate systems than
expected → look for hidden conserved quantities. The Runge-Lenz vector
is the paradigm case. The harmonic oscillator has an analogous hidden
SU(3) symmetry (Fradkin tensor).

## Cross-References

- Landau Vol.1 §48 (Separation of variables)
- Landau Vol.1 §52 (Conditionally-periodic motion)
- Quantum: same separability → same integrable quantum systems
