---
skill_id: convention.units_systems
type: convention
summary_50t: >
  Project default: SI. Complete SI↔Gaussian conversion tables. Replace ε₀→1/(4π),
  μ₀→4π/c² (SI→Gaussian) or reverse. electrodynamics/plasma/optics use SI.
  landau-graph uses Gaussian. Includes Maxwell eqns, potentials, radiation,
  dielectric response, moving media, critical density formula, and common pitfalls.
---

# Unit systems: SI ↔ Gaussian conversion

## Which skills use which

| Skill | Unit system | Standard reference |
|-------|-------------|-------------------|
| `electrodynamics` | SI | Jackson (Ch 1–6) |
| `plasma` | SI | Stix, NRL |
| `optics` | SI | Boyd, Born & Wolf |
| `landau-graph` | Gaussian | Landau-Lifshitz |

When a downstream node cites a landau-graph result, apply the conversion
tables below. Conversion is **exact**: no approximations.

## Fundamental constants

| Quantity | SI | Gaussian |
|----------|-----|----------|
| Coulomb constant | k = 1/(4πε₀) | 1 |
| Vacuum permittivity | ε₀ ≈ 8.854×10⁻¹² F/m | 1/(4π) |
| Vacuum permeability | μ₀ = 4π×10⁻⁷ H/m | 4π/c² |
| Speed of light | c = 1/√(ε₀μ₀) | c |
| Impedance of vacuum | Z₀ = √(μ₀/ε₀) ≈ 377 Ω | 4π/c |

## Conversion tables

### SI → Gaussian

| SI expression | Gaussian equivalent |
|--------------|-------------------|
| ε₀ | 1/(4π) |
| μ₀ | 4π/c² |
| 1/(4πε₀) | 1 |
| μ₀/(4π) | 1/c² |
| √(μ₀/ε₀) | 4π/c |

### Gaussian → SI

| Gaussian expression | SI equivalent |
|--------------------|--------------|
| q₁q₂/r² (force) | q₁q₂/(4πε₀r²) |
| E | √(4πε₀) E_SI |
| B | √(4π/μ₀) B_SI |
| 1 (Coulomb const) | 1/(4πε₀) |

## Maxwell's equations

| | SI | Gaussian |
|---|-----|----------|
| Coulomb | ∇·E = ρ/ε₀ | ∇·E = 4πρ |
| No monopoles | ∇·B = 0 | ∇·B = 0 |
| Faraday | ∇×E = −∂B/∂t | ∇×E = −(1/c) ∂B/∂t |
| Ampère | ∇×B = μ₀J + μ₀ε₀ ∂E/∂t | ∇×B = (4π/c)J + (1/c)∂E/∂t |
| Lorentz force | F = q(E + v×B) | F = q(E + (v/c)×B) |

## Potentials

| | SI | Gaussian |
|---|-----|----------|
| E from potentials | E = −∇φ − ∂A/∂t | E = −∇φ − (1/c)∂A/∂t |
| B from potentials | B = ∇×A | B = ∇×A |
| Wave equation □A | □A = −μ₀J | □A = −(4π/c)J |
| Lorenz gauge | ∇·A + μ₀ε₀ ∂φ/∂t = 0 | ∇·A + (1/c) ∂φ/∂t = 0 |

## Radiation

| | SI | Gaussian |
|---|-----|----------|
| Poynting vector | S = E×H | S = (c/4π) E×B |
| Dipole radiation P | P = μ₀p̈²/(6πc) | P = 2p̈²/(3c³) |
| Larmor formula (non-rel) | P = μ₀q²a²/(6πc) | P = 2q²a²/(3c³) |
| Thomson cross section | σ_T = (8π/3)(μ₀q²/(4πm))² | σ_T = (8π/3)(q²/mc²)² |

## Dielectric / Magnetic response

| | SI | Gaussian |
|---|-----|----------|
| D definition | D = ε₀E + P | D = E + 4πP |
| H definition | H = B/μ₀ − M | H = B − 4πM |
| Polarization P | P = ε₀ χ_e E | P = χ_e E |
| Magnetization M | M = χ_m H | M = χ_m H |
| Permittivity | ε = ε₀(1+χ_e) = ε₀ ε_r | ε = 1 + 4π χ_e |
| Kramers-Kronig (same form!) | ε'(ω)−1 = (2/π)P∫... | ε'(ω)−1 = (2/π)P∫... |

## Moving media (Minkowski)

| | SI | Gaussian |
|---|-----|----------|
| D relation | D + v×H/c² = ε(E + v×B) | D + (v/c)×H = ε(E + (v/c)×B) |
| B relation | B − v×E/c² = μ(H − v×D) | B − (v/c)×E = μ(H − (v/c)×D) |

## Practical plasma formula

Critical density in practical units (common to both systems since n_c is
a number density, not a field):

```
n_c [cm⁻³] = 1.115×10²¹ / λ² [μm²]
```

Derived from ω_p = ω₀ → n_c = ε₀ m_e ω₀² / e² (SI) with ω₀ = 2πc/λ.

## Common pitfalls

1. **4π factors**: The most common error. Gaussian has explicit 4π in Maxwell
   but not in Coulomb's law; SI has 1/(4πε₀) in Coulomb but no 4π in Maxwell.

2. **c in Lorentz force**: Gaussian F = q(E + v×B/c). SI F = q(E + v×B).
   Missing the 1/c leads to errors in relativistic velocity regimes.

3. **Kramers-Kronig is INVARIANT**: The dispersion relations have the SAME form
   in both systems because ε(ω)/ε₀ (SI, dimensionless) and ε(ω) (Gaussian,
   dimensionless) both satisfy K-K identically.

4. **Impedance**: SI has Z₀ ≈ 377 Ω explicitly. Gaussian has Z₀ = 4π/c which
   in practical units is also 377 Ω, but the form obscures the impedance
   concept.

5. **Electric field amplitude conversion**: E_SI ≠ E_G numerically. For plane
   waves: E_G = E_SI / √(4πε₀). A Gaussian-field number plugged directly into
   SI formulas produces wrong powers.

## References

Jackson Appendix §1 (unit conversion tables), Landau Vol 2 §27 (Gaussian
Maxwell), Wikipedia: Gaussian units, NRL Plasma Formulary (critical density).
