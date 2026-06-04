---
skill_id: convention.time_fourier
type: convention
summary_50t: >
  Phase: e^{i(k·r − ωt)}. FT pair: F̃(ω)=∫f(t)e^{+iωt}dt, f(t)=∫(dω/2π)F̃(ω)e^{−iωt}.
  Im(ω)>0 = growth. ñ=n+iκ, κ≥0 absorbing. Causality → ε(ω) analytic in upper half
  ω-plane. Spatial FT opposite sign. Engineering (e^{+jωt}) NOT used.
---

# Time / Fourier convention

**Plane wave**: e^{i(k·r − ωt)}. The wave propagates in direction +k as t
increases.

**Temporal Fourier transform** (paired with the above):

```
F̃(ω) = ∫_{−∞}^{∞} f(t) e^{+iωt} dt        (analysis)
f(t) = ∫_{−∞}^{∞} F̃(ω) e^{−iωt} dω/(2π)  (synthesis)
```

This ensures that f(t) ∝ e^{−iω₀t} maps to F̃(ω) ∝ δ(ω−ω₀), i.e., positive
frequency.

**Spatial Fourier transform** uses the opposite sign (to be consistent with
the spacetime phase factor):

```
F̃(k) = ∫ f(r) e^{−ik·r} d³r,    f(r) = ∫ F̃(k) e^{+ik·r} d³k/(2π)³.
```

## Consequences

- Growing-in-time solutions have **Im(ω) > 0**.
- Causal (retarded) response functions ε(ω), χ(ω), G_ret(ω) are analytic
  in the **upper half ω-plane**.
- Complex refractive index **ñ = n + iκ** with κ ≥ 0 represents absorption:
  e^{ikz} = e^{iñω z/c} = e^{inωz/c} · e^{−κωz/c} → decays in +z.
- Kramers-Kronig relations follow directly from upper-half-plane analyticity.

## Autocorrelation / Wiener-Khinchin

```
Γ(τ) = ⟨E(t+τ) E*(t)⟩ → S(ω) = ∫ Γ(τ) e^{+iωτ} dτ.
```

Sign is +iωτ (not −iωτ) because τ enters Γ on the FIRST argument and the FT
preserves orientation. For monochromatic E = E₀e^{−iω₀t}: Γ(τ)=|E₀|²e^{−iω₀τ},
S(ω)=2π|E₀|² δ(ω−ω₀). Localized at +ω₀ as expected.

## Conversion from engineering convention

Engineering convention uses e^{+jωt}. Conversion: ω ↔ −ω with j ↔ −i. All signs
in the FT pair, plane-wave phase, causality domain, and K-K relations are
reversed. The engineering convention is **NOT used** in any project skill.

If citing an engineering-textbook formula, apply the sign reversal explicitly;
otherwise errors propagate silently in anything involving dispersion or
causality.

## References

Jackson §6.4 (causality, K-K), Boyd §1.2 (FT convention), Landau Vol 8 §82
(K-K), Born & Wolf §10.2 (analyticity).
