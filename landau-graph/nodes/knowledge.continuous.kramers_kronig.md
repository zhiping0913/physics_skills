---
skill_id: knowledge.continuous.kramers_kronig
type: knowledge
summary_50t: >
  ε'(ω)−1 = (1/π)P∫ε''(u)/(u−ω)du. ε''(ω) = −(1/π)P∫[ε'(u)−1]/(u−ω)du.
  Universal for all causal linear response functions. ε(−ω)=ε*(ω).
trigger:
  - checking consistency of ε(ω) data
  - deriving Im ε from measured Re ε (or vice versa)
  - sum rules for oscillator strength
reasoning_role: dispersion_relations
parent: reasoning.causality_to_analyticity
retrieval_cost: 1
---

# knowledge.continuous.kramers_kronig

**Dispersion relations** (Kramers-Kronig):
```
ε'(ω) − 1 = (1/π) P ∫_{-∞}^{∞} ε''(u)/(u−ω) du
ε''(ω)    = −(1/π) P ∫_{-∞}^{∞} [ε'(u)−1]/(u−ω) du
```

**Symmetry**: ε(−ω) = ε*(ω) → ε'(ω) even, ε''(ω) odd.

**Equivalent forms** (using parity, integrating over [0,∞)):
```
ε'(ω) − 1 = (2/π) P ∫_0^∞ u ε''(u)/(u²−ω²) du
ε''(ω)    = −(2ω/π) P ∫_0^∞ [ε'(u)−1]/(u²−ω²) du
```

**Sum rules**:
- f-sum rule: ∫_0^∞ ω ε''(ω) dω = (π/2) ω_p²
- Static limit: ε(0) − 1 = (2/π) ∫_0^∞ ε''(ω)/ω dω
- High-frequency: ε'(ω) → 1 − ω_p²/ω² for ω → ∞

**Origin**: Causality (f(τ)=0 for τ<0) → analyticity in UHP → Cauchy integral.

**Asymmetry** (§82): Using (82.8) to get ε' from ε'' is SAFE — any ε''>0 gives a
physically possible ε'. Using (82.7) to get ε'' from ε' is NOT safe — it does not
automatically guarantee ε''>0. For data analysis, always use the safe direction.

**For conductors**: ε(ω) ~ 4πiσ/ω at low ω. The ω=0 pole introduces
an extra term in the ε'' relation:
ε''(ω) = −(1/π) P ∫₋∞^∞ ε'(x)/(x−ω) dx + 4πσ/ω   (82.9)
For the K-K with subtraction:
ε'(ω) − ε'(0) = (2ω²/π) P ∫₀^∞ ε''(u)/[u(u²−ω²)] du.

**Oscillator strength** (§82, (82.10-82.11)): Standard dispersion form:
ε'(ω) − 1 = −(4πe²/m) ∫₀^∞ f(x)/(ω²−x²) dx
where f(ω) = (m/2π²e²) ω ε''(ω) is the oscillator strength density.
f-sum rule: ∫₀^∞ f(ω) dω = N (total electron number density).

- Landau Vol.8 §82
