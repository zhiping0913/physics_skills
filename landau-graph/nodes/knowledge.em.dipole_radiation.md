---
skill_id: knowledge.em.dipole_radiation
type: knowledge
summary_50t: >
  For a ≪ λ: dI/dΩ = (d̈²/4πc³)sin²θ. Total power: I = 2d̈²/3c³.
  Dipole moment d = Σ er. Larmor formula: I = 2e²a²/3c³ for one charge.
trigger:
  - non-relativistic radiation
  - small source, arbitrary charge distribution
  - need angular distribution and total power
reasoning_role: leading_multipole
parent: reasoning.multipole_expansion_radiation
retrieval_cost: 1
---

# knowledge.em.dipole_radiation

**Condition**: a ≪ λ (source small compared to wavelength)

**Dipole moment**: d = Σ e_a r_a = ∫ ρ r dV

**Radiation field** (far zone, R₀ ≫ λ):
```
H = [d̈×n]/c²R₀      E = [[d̈×n]×n]/c²R₀
```

**Angular distribution**: dI/dΩ = (d̈²/4πc³) sin²θ
(Toroidal pattern: zero along dipole axis, max in equatorial plane)

**Total power** (Larmor for one charge): I = 2d̈²/3c³ = 2e²a²/3c³

**Spectral decomposition** (periodic motion):
d(t) = Σ d_n e^{−inω₀t} → I_n = (4ω₀⁴n⁴/3c³)|d_n|²

**When dipole vanishes** (symmetry-forbidden): next order = magnetic dipole
(∝ m̈) + electric quadrupole (∝ Q̈). These are ∝ (a/λ)² smaller.

- Landau Vol.2 §67-68
