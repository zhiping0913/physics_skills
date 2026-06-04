---
skill_id: convention.plasma_parameters
type: convention
summary_50t: >
  Standard plasma parameter definitions for SI and Gaussian MHD, including β,
  normalized vector potential a₀, and critical density n_c with conversion rules
  across unit systems.
---

# Plasma parameter conventions

This node captures the commonly used plasma parameter definitions in both SI
and Gaussian unit systems, focusing on parameters where confusion arises:
plasma beta, the normalized laser amplitude a₀, and critical density n_c.

## Plasma beta

**SI (MHD)**: β = 2μ₀p/B²
**Gaussian**: β = 8πp/B²

Both definitions are unitless and numerically identical when the correct p and B
values are used in the respective systems.

## Normalized vector potential a₀

For **linear polarization**:

```
a₀ = e E_peak / (m_e ω₀ c)
```

At λ = 1 μm, the practical formula is:

```
a₀ ≈ 0.85 √(I / [10¹⁸ W/cm²])
```

For **circular polarization** (same intensity I):

```
a₀_circ = a₀ / √2
```

Reason: circularly polarized light splits its electric field amplitude equally
between two orthogonal components, reducing the peak field along any single axis
by 1/√2.

## Critical density

**SI**:

```
n_c = ε₀ m_e ω² / e²
```

**Practical formula**:

```
n_c [cm⁻³] = 1.115 × 10²¹ / λ² [μm²]
```

**Gaussian**: `n_c = m_e ω² / (4π e²)`

When crossing the landau-graph boundary, apply the Gaussian form using the
conversion rules in [[convention.units_systems]] (within this skill).

**References**: Gibbon (2005), Kruer (1988), NRL Plasma Formulary.
