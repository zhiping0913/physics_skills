---
skill_id: knowledge.continuous.dielectric_dispersion
type: knowledge
summary_50t: >
  D(t) = E(t) + ∫₀^∞ f(τ)E(t−τ)dτ. For e^{−iωt}: D = ε(ω)E.
  ε(ω) complex: ε'(ω) dispersion, ε''(ω) absorption. ε(∞) = 1.
  Conductors: ε(ω) ~ 4πiσ/ω at low ω.
trigger:
  - frequency-dependent dielectric response
  - dissipation in EM fields inside matter
  - optical properties (refractive index, absorption)
reasoning_role: frequency_dispersion
parent: reasoning.causality_to_analyticity
retrieval_cost: 1
---

# knowledge.continuous.dielectric_dispersion

**Linear response** (causal, local in space):
```
D(t) = E(t) + ∫_0^∞ f(τ) E(t−τ) dτ
D = ε̂ E (operator notation)
```

**Monochromatic fields**: D = ε(ω)E,
```
ε(ω) = 1 + ∫_0^∞ f(τ) e^{iωτ} dτ
ε(ω) = ε'(ω) + iε''(ω),  ε'(ω) even, ε''(ω) odd
```

**Key limits**:
| Regime | ε(ω) |
|--------|------|
| ω→0 (dielectric) | ε(ω) → ε₀ (static) |
| ω→0 (conductor) | ε(ω) → 4πiσ/ω |
| ω→∞ | ε(ω) → 1 (no time for polarization) |
| ω ≫ ω_atomic | ε(ω) ≈ 1 − ω_p²/ω² |

**Dissipation**: Q = (ω/8π) ε''(ω) |E|². ε'' > 0 for absorption (second law).
In transparent regions: ε'' ≪ ε' (never truly zero!), energy density
U = ∂(ωε')/∂ω · |E|²/8π. **Crucial caveat (§80): in general absorbing media,
NO thermodynamic definition of EM energy is possible** — the dispersive
energy formula only applies when absorption is negligible.

**Sign constraints**: ε'' > 0 always (bodies in thermodynamic equilibrium).
ε' has NO sign constraint — can be positive or negative (§80).

**Conditions for macroscopic description**: λ ≫ a (atomic size),
ω not in anomalous skin effect regime (metals).
**Poynting vector**: S = (c/4π)[E×H] remains valid even with dispersion (§80).

- Landau Vol.8 §77-82
