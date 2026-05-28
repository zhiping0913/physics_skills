---
skill_id: reasoning.multipole_expansion_radiation
type: reasoning
summary_50t: >
  When source size a ≪ λ, the retarded time variation across the source
  is negligible. The radiation field is dominated by the lowest non-vanishing
  multipole — usually electric dipole ∝ p̈.
trigger:
  - radiation from compact source (a ≪ λ)
  - need leading-order radiation field
  - small source compared to wavelength
reasoning_role: scale_separation
parent: reasoning.retarded_green_function
children:
  - knowledge.em.dipole_radiation
  - knowledge.em.quadrupole_radiation
related:
  - reasoning.small_parameter_expansion
retrieval_cost: 1
---

# reasoning.multipole_expansion_radiation — Small Source → Multipole Expansion

## Core Picture

When the source size a is much smaller than the radiated wavelength λ,
the phase variation e^{ikr} across the source is negligible (kr ≪ 1).
The retarded potentials can be expanded in powers of a/λ.

The leading term is the electric dipole: the source's charge distribution
oscillates as a whole, with dipole moment d̈ producing radiation.
If the dipole vanishes (symmetry-forbidden), the next terms are magnetic
dipole and electric quadrupole.

## Algorithm

```
1. Check condition: a ≪ λ = 2πc/ω
2. Write retarded potential: A = (1/cR₀)∫ j(t−R₀/c + n·r/c) dV
3. Expand j in retarded time argument: j(t' + n·r/c) ≈ j(t') + (n·r/c)∂j/∂t' + ...
4. First term: ∫ j dV = Σ ev = ḋ → electric dipole radiation
5. Second term: splits into magnetic dipole (∝ m̈) and electric quadrupole (∝ Q̈)
6. Far field: E, H ∝ 1/R₀ (radiation zone), H = [n×Ȧ]/c
7. Angular distribution: dI/dΩ ∝ sin²θ for dipole (toroidal pattern)
```

## Validity Condition

```
a ≪ λ    (source much smaller than wavelength)
R₀ ≫ λ   (observer in radiation zone)
```

## Why a/λ is the Key Parameter

The time for light to cross the source is a/c. The oscillation period is
T = 2π/ω = λ/c. The condition a/c ≪ T is exactly a ≪ λ.

When a/λ is not small: need full retarded potential integration.
When v/c is not small (relativistic charges): Liénard-Wiechert formula needed.

## Cross-References
- Landau Vol.2 §67 (dipole), §71 (quadrupole and magnetic dipole)
- Landau Vol.1 §22: same scale-separation logic (small amplitude → quadratic)
- See wiki: dipole-approximation for plasma HHG applications
