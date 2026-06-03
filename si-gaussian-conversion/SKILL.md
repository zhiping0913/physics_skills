---
name: si-gaussian-conversion
description: "Complete SI ↔ Gaussian unit conversion for electrodynamics. Replace ε₀, μ₀, c factors when translating between Jackson (SI), Landau (Gaussian), and other sources. Essential when using landau-graph (Gaussian) alongside electrodynamics skill (SI)."
---

# SI ↔ Gaussian Unit Conversion for Electrodynamics

When using `landau-graph` (Gaussian units, following Landau-Lifshitz) alongside
the `electrodynamics` skill (SI units, following Jackson, Griffiths), formulas
differ by factors of 4πε₀, c, and μ₀/4π. This reference provides the systematic
translation.

## Fundamental Constants

| Quantity | SI | Gaussian |
|----------|-----|----------|
| Coulomb constant | k = 1/(4πε₀) | 1 |
| Vacuum permittivity | ε₀ | 1/(4π) |
| Vacuum permeability | μ₀ = 4π×10⁻⁷ H/m | 4π/c² |
| Speed of light | c = 1/√(ε₀μ₀) | c |
| Impedance of vacuum | Z₀ = √(μ₀/ε₀) ≈ 377 Ω | 4π/c |

## How to Convert

Replace ALL occurrences of ε₀ and μ₀ according to the table below,
then set the remaining c factors. The conversion is EXACT — no approximations.

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

## Core Equations: Both Systems

### Maxwell's Equations

| | SI | Gaussian |
|---|-----|----------|
| Coulomb | ∇·E = ρ/ε₀ | ∇·E = 4πρ |
| No monopoles | ∇·B = 0 | ∇·B = 0 |
| Faraday | ∇×E = −∂B/∂t | ∇×E = −(1/c)∂B/∂t |
| Ampère | ∇×B = μ₀J + μ₀ε₀∂E/∂t | ∇×B = (4π/c)J + (1/c)∂E/∂t |
| Lorentz force | F = q(E + v×B) | F = q(E + (v/c)×B) |

### Potentials

| | SI | Gaussian |
|---|-----|----------|
| E from potentials | E = −∇φ − ∂A/∂t | E = −∇φ − (1/c)∂A/∂t |
| B from potentials | B = ∇×A | B = ∇×A |
| Wave equation □A | □A = −μ₀J | □A = −(4π/c)J |
| Lorenz gauge | ∇·A + μ₀ε₀∂φ/∂t = 0 | ∇·A + (1/c)∂φ/∂t = 0 |

### Radiation

| | SI | Gaussian |
|---|-----|----------|
| Poynting vector | S = E×H | S = (c/4π) E×B |
| Dipole radiation P | P = μ₀p̈²/(6πc) | P = 2p̈²/(3c³) |
| Larmor formula (non-rel) | P = μ₀q²a²/(6πc) | P = 2q²a²/(3c³) |
| Thomson cross section | σ_T = (8π/3)(μ₀q²/(4πm))² | σ_T = (8π/3)(q²/mc²)² |

### Dielectric/Magnetic Response

| | SI | Gaussian |
|---|-----|----------|
| D definition | D = ε₀E + P | D = E + 4πP |
| H definition | H = B/μ₀ − M | H = B − 4πM |
| Polarization P | P = ε₀χ_e E | P = χ_e E |
| Magnetization M | M = χ_m H | M = χ_m H |
| ε = ε₀(1+χ_e) | ε = ε₀ε_r | ε = 1 + 4πχ_e |
| Kramers-Kronig (same form!) | ε'(ω)−1 = (2/π)P∫... | ε'(ω)−1 = (2/π)P∫... |

### Moving Media (Minkowski)

| | SI | Gaussian |
|---|-----|----------|
| D + v×H/c² = | ε(E + v×B) | D + (v/c)×H = ε(E + (v/c)×B) |
| B − v×E/c² = | μ(H − v×D) | B − (v/c)×E = μ(H − (v/c)×D) |

## Common Pitfalls

1. **4π factors**: The most common error — Gaussian has explicit 4π in Maxwell
   but not in Coulomb's law; SI has 1/(4πε₀) in Coulomb but no 4π in Maxwell.

2. **c in Lorentz force**: Gaussian F = q(E + v×B/c). SI F = q(E + v×B).
   Missing the 1/c leads to errors in relativistic velocity regimes.

3. **Kramers-Kronig is INVARIANT**: The dispersion relations have the SAME form
   in both systems because ε(ω) is dimensionless in Gaussian and ε(ω)/ε₀ is
   dimensionless in SI. The conversion cancels out.

4. **Impedance**: SI has Z₀≈377Ω explicitly. Gaussian has Z₀=4π/c which in
   practical units is also 377Ω, but the form obscures the impedance concept.

5. **The `electrodynamics` skill uses SI** (following Jackson, Griffiths).
   **The `landau-graph` skill uses Gaussian** (following Landau).
   When agents use BOTH skills, apply the conversion table above.

## Reference

- Wikipedia: https://en.wikipedia.org/wiki/Gaussian_units
- Jackson, Appendix §1 (unit conversion tables)
- Landau Vol.2 §27 (Gaussian Maxwell equations)
