---
skill_id: convention.nonlinear_susceptibility
type: convention
summary_50t: >
  χ⁽n⁾ follows Boyd §1.5 (degenerate Butcher-Cotter): P^(n)(ω_s) = ε₀ Σ K χ⁽n⁾
  E₁…E_n, K = degeneracy factor. n₂ = (3/4n₀²ε₀c) Re[χ⁽³⁾₁₁₁₁], Maker-Terhune 3/4.
  d_il = (1/2)χ⁽²⁾_ijk (contracted index). SHG efficiency: CW intensity; for
  pulsed use ∫|A|⁴dt/(∫|A|²dt)².
---

# Nonlinear susceptibility convention

## Polarization expansion (Boyd §1.5, degenerate Butcher-Cotter)

The nonlinear polarization in the **frequency domain** is:

```
P_i^(n)(ω_σ) = ε₀ Σ_{α₁…α_n} K(ω_σ; ω₁,…,ω_n)
               χ⁽n⁾_{i j₁…j_n}(ω_σ; ω₁,…,ω_n) E_{j₁}(ω₁)…E_{j_n}(ω_n)
```

where ω_σ = ω₁ + … + ω_n and K is the **degeneracy factor**:

```
K = 2^{m+n−p} n! / (n_1! n_2! …)
```

with:
- n = order of nonlinearity (2, 3, …)
- m = number of zero-frequency (DC) fields
- p = 0 if ω_σ = 0, p = 1 if ω_σ ≠ 0
- n_k = number of identical frequencies in the set {ω₁,…,ω_n}

**Common values of K**:
| Process | Frequencies | K |
|---------|------------|---|
| SHG | ω+ω → 2ω | 1/2 |
| Sum-frequency | ω₁+ω₂ → ω₃ (ω₁≠ω₂) | 1 |
| THG | ω+ω+ω → 3ω | 1/4 |
| Kerr (self) | ω−ω+ω → ω | 3/4 |
| DC Kerr | 0+ω → ω | 3 |

## Second-order: d-matrix (contracted index)

In contracted notation (Boyd §1.5, Table 1.5.1):

```
d_{il} = (1/2) χ⁽²⁾_{ijk}
```

where l = 1…6 is the Voigt contraction of (j,k). Specifically:

| jk | 11 | 22 | 33 | 23,32 | 31,13 | 12,21 |
|----|----|----|----|-------|-------|-------|
| l  | 1  | 2  | 3  | 4     | 5     | 6     |

The factor 1/2 is **Boyd's convention**. Some authors (Butcher-Cotter, Shen)
omit this 1/2 and define d_{il} = χ⁽²⁾_{ijk} directly. When citing d-matrix
values from different sources, check the convention or expect factor-2 errors.

## Third-order: n₂ formula (Maker-Terhune convention)

The nonlinear refractive index for a single-frequency beam:

```
n₂ = (3 / 4 n₀² ε₀ c) Re[ χ⁽³⁾_{1111}(−ω; ω, −ω, ω) ]
```

The factor **3/4** is the **Maker-Terhune convention** and arises from:
- K = 3/4 for degenerate self-action (ω−ω+ω → ω)
- The relationship between intensity |E|² and P^(3) in the wave equation.

Without the K factor, the "bare" formula n₂ ∝ χ⁽³⁾/(n₀²ε₀c) would differ by
4/3. Always confirm which n₂ definition a source uses before comparing values.

## SHG efficiency

For CW (continuous wave) plane-wave SHG:

```
η = P_{2ω} / P_ω = tanh²( Γ L )
```

where Γ ∝ d_eff. In the low-conversion limit: η ∝ |d_eff|² L² I_ω.

For **pulsed** SHG, multiply the CW efficiency by the temporal factor:

```
η_pulsed = η_CW × ( ∫ |A(t)|⁴ dt / (∫ |A(t)|² dt)² )
```

For Gaussian pulses: factor = 1 / (√2 τ₀ √π). This temporal enhancement factor
is independent of the d-matrix convention but must be applied when comparing
pulsed SHG data to CW formulas.

## References

Boyd §1.5 (Butcher-Cotter convention, K factors), Boyd §4.1 (n₂ definition,
Maker-Terhune 3/4), Shen §2.1 (alternative d-matrix convention without 1/2),
Butcher & Cotter (1990) "The Elements of Nonlinear Optics" (degeneracy factors).
