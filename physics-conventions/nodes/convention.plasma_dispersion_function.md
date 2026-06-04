---
skill_id: convention.plasma_dispersion_function
type: convention
summary_50t: >
  Z(ζ) = π^{−½} ∫_{−∞}^{∞} e^{−x²}/(x−ζ) dx (Fried-Conte normalization, Stix §8).
  Contour bent BELOW singularity for Im(ζ)>0 (causal Landau prescription). Analytic
  continuation to lower half-plane via Landau rule. Asymptotic: Z(ζ) ~ i√π e^{−ζ²}
  −1/ζ −1/(2ζ³) −3/(4ζ⁵). Z'(ζ) = −2(1+ζ Z(ζ)).
---

# Plasma dispersion function Z(ζ)

## Definition (Fried-Conte normalization)

The plasma dispersion function, introduced by Fried & Conte (1961), is:

```
Z(ζ) = (1/√π) ∫_{−∞}^{∞} e^{−x²} / (x − ζ) dx          Im(ζ) > 0
```

This is the **project default** and follows Stix §8. The normalization
(π^{−½}) ensures Z(0) = i√π.

## Landau contour prescription

For **Im(ζ) > 0**, the integration is along the real x-axis. The singularity
at x = ζ lies in the upper half-plane and the contour passes below it — this
is the **causal (Landau)** prescription.

For **Im(ζ) ≤ 0**, the function is defined by **analytic continuation** from
the upper half-plane. The Landau contour is bent **below** the pole, picking
up the residue:

```
Z(ζ) = (1/√π) P ∫_{−∞}^{∞} e^{−x²}/(x−ζ) dx + i√π e^{−ζ²}          Im(ζ) ≤ 0
```

where P denotes the Cauchy principal value.

## Properties

**Derivative**:
```
Z'(ζ) = −2 (1 + ζ Z(ζ))
```

This follows from integration by parts and is used ubiquitously in kinetic
plasma dispersion relations.

**Symmetry**:
```
Z(−ζ) = −Z(ζ) + 2i√π e^{−ζ²}
Z*(ζ) = Z(ζ*)          (complex conjugate)
```

## Asymptotic expansion (|ζ| ≫ 1)

For large argument (cold-plasma / fluid limit), Im(ζ) > 0:

```
Z(ζ) ~ i√π e^{−ζ²} − 1/ζ − 1/(2ζ³) − 3/(4ζ⁵) − 15/(8ζ⁷) − …
```

The i√π e^{−ζ²} term represents Landau damping. For Im(ζ) → 0 (marginally
damped), this term becomes i√π e^{−ζ_R²} where ζ_R = Re(ζ).

The algebraic series (1/ζ, 1/(2ζ³), …) gives the fluid (cold/hot-plasma)
expansion; keeping more terms adds finite-Larmor-radius corrections.

## Power-series expansion (|ζ| ≪ 1)

For small argument (warm-fluid / highly-damped regime):

```
Z(ζ) = i√π e^{−ζ²} − 2ζ + (4/3)ζ³ − (8/15)ζ⁵ + …
```

## Alternative normalizations (not used in project)

Some sources define Z without the π^{−½} factor or with a different sign in
the denominator. Common alternatives:

| Source | Definition | Conversion |
|--------|-----------|------------|
| Fried-Conte (project) | π^{−½} ∫ e^{−t²}/(t−ζ) dt | — |
| Ichimaru | (1/√π) ∫ e^{−t²}/(t−ζ) dt | same as project |
| Swanson | same as Fried-Conte | same as project |
| Some Russian texts | ∫ e^{−t²}/(t−ζ) dt (no 1/√π) | multiply by 1/√π |

Always verify the normalization when comparing dispersion-relation
coefficients across sources.

## References

Fried & Conte (1961), "The Plasma Dispersion Function", Academic Press.
Stix §8 (kinetic dispersion, Z function), Swanson §4.2 (Landau contour,
analytic continuation), Ichimaru §4.3 (plasma dispersion function properties).
