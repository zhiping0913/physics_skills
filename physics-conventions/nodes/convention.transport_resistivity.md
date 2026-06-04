---
skill_id: convention.transport_resistivity
type: convention
summary_50t: >
  Spitzer resistivity with electron-electron correction factor: η_∥(Spitzer) =
  0.51 × η_∥(Lorentz) for Z=1, tending to 1.0 as Z→∞. Includes lnΛ definition
  and SI/Gaussian conversion.
---

# Transport resistivity conventions

Resistivity in a fully ionized plasma is described by the Spitzer (Spitzer-Härm)
formula. The central convention issue is the electron-electron correction factor
and its Z-dependence.

## Basic Braginskii resistivity

The parallel resistivity from the Braginskii transport equations:

```
η_∥ = m_e ν_ei / (n e²)
```

This is the Lorentz-gas result (ions are fixed scattering centers, electrons do
not interact with each other).

## Spitzer-Härm correction

For Z = 1, the electron-electron (e-e) collisions add a correction:

```
η_∥(Spitzer) = 0.51 × η_∥(Lorentz gas)    for Z = 1
```

The 0.51 factor is baked into the standard numerical formula:

```
η_∥ ≈ 5.2 × 10⁻⁵ · Z · lnΛ / T_e[eV]^{3/2}  [Ω·m]
```

For **Z → ∞** (Lorentz gas limit): the correction factor → 1.0.
For intermediate Z: see the tabulated correction in Spitzer §5.

## Coulomb logarithm

```
lnΛ = ln(λ_D / b_min)
b_min = max(b_classical, b_quantum)
```

where λ_D is the Debye length, b_classical = Ze²/(4πε₀ k_B T_e), and b_quantum =
ħ/(m_e v_th). At high densities/temperatures where b_quantum > b_classical, the
quantum-mechanical cutoff applies.

When converting to Gaussian, η_∥ carries units of seconds, and the formula
changes by factors of 4π.

**References**: Spitzer (1956) Physics of Fully Ionized Gases, Braginskii
(1965), NRL Plasma Formulary.
