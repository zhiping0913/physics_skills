---
skill_id: convention.scattering_amplitude
type: convention
summary_50t: >
  Scattering amplitude f(k,k') with dσ/dΩ = |f|², optical theorem σ_ext =
  (4π/k) Im[f(k,k)], and Born approximation in both SI and Gaussian
  normalizations.
---

# Scattering amplitude conventions

The scattering amplitude normalization determines the relationship between
differential cross-section and the amplitude itself, as well as the form of the
optical theorem and the Born approximation.

## Asymptotic form

For an incident plane wave E₀ e^{ikz} scattering from a target:

```
E_s(r) → f(k, k') E₀ e^{ikr} / r    as r → ∞
```

where k is the incident wavevector (magnitude k = |k|), k' is the scattered
direction, and r is the radial distance from the target.

## Differential cross-section

```
dσ/dΩ = |f(k, k')|²
```

This normalization is SI-compatible with the Green's function convention
(∇² + k²)G = −δ(r).

## Optical theorem

```
σ_ext = (4π/k) Im[ f(k, k) ]
```

The **forward** scattering amplitude (k' = k) determines the total extinction
cross-section. This is a consequence of energy conservation.

## Born approximation

**SI**:

```
f(k, k') = (k²/4π) ∫ [ε(r')/ε₀ − 1] e^{i(k − k')·r'} d³r'
```

**Gaussian**: The factor k²/(4π) is replaced by k² (i.e., the 1/4π is dropped):

```
f_G(k, k') = k² ∫ [ε(r') − 1] e^{i(k − k')·r'} d³r'
```

When bridging from landau-graph (Gaussian) results, multiply amplitudes by
1/4π where appropriate.

**References**: Jackson §10, Newton (2002) Scattering Theory, Sakurai (1994)
Modern Quantum Mechanics.
