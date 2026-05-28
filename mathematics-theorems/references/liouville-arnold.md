# Liouville-Arnold Theorem

**Statement**: A Hamiltonian system with n degrees of freedom is completely
integrable (solvable by quadratures) iff it has n independent integrals of
motion F_1,...,F_n that are in involution: {F_i, F_j} = 0 for all i,j.

**Used in**: `reasoning.separation_of_variables` (Vol.1 §52)

## For Closed Mechanical Systems

Total integrals: 2s−1. Additive: 7 (E, P, M). Non-additive: 2s−8.
Complete integrability needs s integrals in involution. Since additive
integrals don't all commute ({M_i,M_j}=ε_{ijk}M_k), need {E,M²,M_z} etc.

## Proof Sketch

Level sets M_f = {x: F_i(x)=f_i} are n-dim invariant tori. Construct
action-angle variables (I,φ) with H=H(I), φ̇=ω(I)=const. Motion is
conditionally periodic on n-torus. Solution: I_i(t)=const, φ_i(t)=ω_i t+φ_i(0).

## Failure
Fewer than n involutive integrals → non-integrable (generic, chaotic).
Example: 3-body problem (n=3) has 10 integrals but not enough involutive ones.

## References
- Landau & Lifshitz, Mechanics, §52
- Arnold, Mathematical Methods of Classical Mechanics, Ch. 10
