# Bertrand's Theorem

**Statement**: Only U ∝ −1/r (Kepler/Coulomb) and U ∝ r² (harmonic oscillator)
give strictly closed orbits for ALL finite bound states in a central potential.

**Used in**: `reasoning.conservation_to_effective_reduction` (Vol.1 §14)

## Proof Sketch

**Step 1**: Orbit equation for central potential U(r) with angular momentum M:
dφ = (M/r²)dr / √[2m(E−U) − M²/r²]
Angular advance per radial period: Δφ = 2∫_{r_min}^{r_max} ...

**Step 2**: Expand around circular orbit r₀ satisfying U'(r₀) = M²/(mr₀³).
For nearly circular orbits, small oscillations in r have frequency:
ω_r² = U''(r₀)/m + 3M²/(m²r₀⁴).
Angular frequency: ω_φ = M/(mr₀²).

**Step 3**: For all bound orbits to close, ω_φ/ω_r must be CONSTANT,
independent of r₀ (and thus of M, E). This gives a differential equation
for U(r): r·U'' + 3(1−1/R²)·U' = 0, where R = ω_φ/ω_r.

**Step 4**: Solutions: U(r) = A·r^{3/R²−2} + B. For closed bound orbits
with rational Δφ/2π = m/n = 1/R, only two integer possibilities work:
R²=1 → U∝r² (harmonic oscillator, Δφ=π)
R²=1/4 → U∝−1/r (Kepler, Δφ=2π)

## References
- Landau & Lifshitz, Mechanics, §14, Appendix
- Goldstein, Classical Mechanics, 3rd ed., §3.6
