---
skill_id: reasoning.causality_to_analyticity
type: reasoning
summary_50t: >
  Response cannot precede cause → f(τ)=0 for τ<0 → ε(ω) analytic in
  upper half-plane → Kramers-Kronig: Re ε and Im ε are Hilbert transforms.
  This is universal for ALL linear response functions.
trigger:
  - need to relate real and imaginary parts of a response function
  - causal linear system → what constraints on the response?
  - checking consistency of measured ε(ω) data
reasoning_role: causality_constraint
parent: reasoning.causality_as_constraint
children:
  - knowledge.continuous.kramers_kronig
  - knowledge.continuous.dielectric_dispersion
retrieval_cost: 1
---

# reasoning.causality_to_analyticity — Causality → Analytic ε(ω) → Kramers-Kronig

## Core Picture

The response of a medium to an EM field is causal: D(t) depends on E(t−τ)
for τ ≥ 0 only. This single physical fact has profound consequences:

1. ε(ω) = 1 + ∫₀^∞ f(τ) e^{iωτ} dτ is analytic in the UPPER half-plane.
   The E(t) term is separated explicitly in (77.3) to avoid a δ-function
   singularity in f(τ) at τ=0 (§82 footnote).
2. ε(ω) has NO singularities for Im ω > 0, and NO zeros in the UHP.
   On the imaginary axis: ε(ω) is real, monotonically decreasing from ε₀>1
   (or +∞ for metals) at ω=i0 to 1 at ω=i∞.
3. This forces a universal relation between Re ε and Im ε — the Kramers-Kronig
   dispersion relations.

## Algorithm

```
1. Write D(t) = E(t) + ∫₀^∞ f(τ)E(t−τ)dτ (causality: integral from 0 to ∞)
2. For monochromatic field: D = ε(ω)E, ε(ω) = 1 + ∫₀^∞ f(τ)e^{iωτ}dτ
3. Since the integral converges for Im ω > 0, ε(ω) is analytic in UHP
4. Apply Cauchy's theorem to ε(ω)−1 on a contour along real axis + large semicircle:
   ε(ω) − 1 = (1/iπ) P ∫[ε(u)−1]/(u−ω) du
5. Separate real and imaginary parts:
   ε'(ω) − 1 = (1/π) P ∫ ε''(u)/(u−ω) du
   ε''(ω) = −(1/π) P ∫ [ε'(u)−1]/(u−ω) du
```

**Asymmetry of KK**: (82.8) → ε' from ε'' is "safe" — any ε''>0 yields a
physically possible ε'. (82.7) → ε'' from ε' does NOT guarantee ε''>0.
This is crucial for data analysis: always use (82.8), never (82.7) to infer.

## Universal Application

This reasoning applies to ANY linear response function:
- Dielectric permittivity ε(ω)
- Magnetic permeability μ(ω)
- Conductivity σ(ω)
- Generalized susceptibility α(ω)
- Scattering amplitudes (forward dispersion relations)

## Key Properties

- ε(−ω*) = ε*(ω) for complex ω (82.2) → ε(iω'') is real on the imaginary axis
  (generalizes ε(−ω)=ε*(ω) from §77 which holds only for real ω)
- ε'(ω) even, ε''(ω) odd for real ω
- ε(∞) = 1 (no medium can respond at infinite frequency)
- For conductors: ε(ω) ~ i·4πσ/ω at low frequency (ω→0 pole), 
  f(τ)−4πσ→0 at τ→∞ (not f(τ) itself)
- Sum rule: ∫₀^∞ ω ε''(ω) dω = (π/2)ω_p² (oscillator strength)
- For metals when ε(ω) loses physical meaning due to spatial dispersion:
  use solution of formal problem with spatially homogeneous field (§82)

## Cross-References
- Landau Vol.8 §77 (dispersion), §82 (analytic properties)
- Landau Vol.5 §123 (generalized susceptibility, fluctuation-dissipation)
- Landau Vol.10 §29: plasma ε(k,ω) satisfies same analyticity
