---
skill_id: reasoning.em.antenna_radiation_pattern
type: reasoning
summary_50t: >
  Given J(r)e^{−iωt} on antenna: radiation-zone approximation |r−r'|≈r−n·r'
  → A ≈ (μ₀/4πr)e^{ikr}∫J(r')e^{−ik·r'}dV' → E,B ∝ 1/r → dP/dΩ from Poynting.
  Directivity, gain, radiation resistance follow.
trigger:
  - computing radiation from known antenna current distribution
  - designing antenna for specific radiation pattern
  - calculating power radiated into specific direction
reasoning_role: antenna_radiation
parent: reasoning.multipole_expansion_radiation
retrieval_cost: 1
references:
  - landau-graph: reasoning.multipole_expansion_radiation
  - landau-graph: knowledge.em.dipole_radiation
---

# reasoning.em.antenna_radiation_pattern — Current Distribution → Far Field

## Core Picture

Given a known time-harmonic current distribution J(r, t) = Re[J(r)e^{−iωt}]
on an antenna structure, the radiation fields in the FAR ZONE (r ≫ λ, r ≫ D
where D is antenna size) are obtained by expanding the retarded potential
integral in powers of 1/r:

**Algorithm** (Jackson §9.2-9.8):

```
1. Vector potential in radiation zone (|r| ≫ |r'|):
   A(r) ≈ (μ₀/4π) (e^{ikr}/r) ∫ J(r') e^{−ik n·r'} dV'
   where k = ω/c, n = r/r is the observation direction.

2. Radiation fields (keep only ∝ 1/r terms):
   B = ∇×A ≈ ik n×A,    E = ic/k ∇×B ≈ −c n×B (plane-wave relation)

3. Time-averaged Poynting vector:
   ⟨S⟩ = (c/2μ₀)|B|² n = (μ₀ck²/32π²r²) |∫ J(r')e^{−ik·r'} dV'|² n

4. Angular power distribution:
   dP/dΩ = r² ⟨S⟩ = (μ₀ck²/32π²) |∫ J(r')e^{−ik·r'} dV'|²

5. Total radiated power: P = ∫ (dP/dΩ) dΩ
   Radiation resistance: R_rad = 2P/|I₀|²
   Directivity: D(θ,φ) = (dP/dΩ) / (P/4π)
```

## Key Examples

**Hertzian dipole** (dl ≪ λ, uniform current I₀):
Radiation resistance: R_rad = 80π²(dl/λ)² Ω ≈ 790(dl/λ)² Ω
Pattern: dP/dΩ ∝ sin²θ (doughnut shape)

**Half-wave dipole** (L = λ/2, I(z) = I₀ cos(πz/L)):
Input impedance ≈ 73 + j42.5 Ω
Pattern: dP/dΩ ∝ [cos(π/2 cos θ)/sin θ]²

**Antenna arrays** (N identical elements with spacing d):
Array factor: AF(θ) = Σ e^{i(n−1)kd cos θ}
Total pattern = (element pattern) × (array factor)
Grating lobes appear when kd sin θ > 2π

## Connection to Multipole Expansion

The radiation-zone current integral is the CONVERSE of the multipole
expansion: in multipole expansion (landau-graph), we expand the source
in powers of kr' ≪ 1. Here, we compute the EXACT radiation integral
(no expansion in kr') — this is needed when antenna size ∼ λ.

## Cross-References

- Jackson §9.2-9.8
- Griffiths §11.1-11.4
- landau-graph: reasoning.multipole_expansion_radiation (expands in kr'≪1)
- landau-graph: knowledge.em.dipole_radiation (Hertzian dipole as special case)
