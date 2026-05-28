---
skill_id: reasoning.linear_response_general
type: reasoning
summary_50t: >
  For ANY causal linear response A(ω)=χ(ω)F(ω): χ(ω) analytic in UHP →
  Kramers-Kronig. Unifies dielectric, magnetic, mechanical, density, and
  conductivity susceptibilities across V5,V8,V9,V10.
trigger:
  - computing linear response of any system to weak external perturbation
  - need dispersion relations for a susceptibility function
  - relating real (dispersive) and imaginary (dissipative) parts of response
reasoning_role: universal_linear_response
parent: reasoning.causality_as_constraint
children:
  - reasoning.causality_to_analyticity
  - reasoning.fluctuation_dissipation_quantum
  - reasoning.spatial_dispersion
retrieval_cost: 1
---

# reasoning.linear_response_general — Universal Linear Response Theory

## Core Picture

When a physical system is subjected to a weak external perturbation F(t),
its response A(t) is linear:

```
A(t) = ∫_{-∞}^{t} χ(t−t') F(t') dt'
```

Causality (χ(τ<0)=0) forces χ(ω) to be analytic in the upper half-plane.
This single fact leads to universal relations between the real (dispersive)
and imaginary (dissipative) parts of the susceptibility.

This is NOT specific to dielectrics. It applies to EVERY linear response
function in physics. The agent should recognize: whenever you see
"generalized susceptibility," "response function," or "Green's function,"
the SAME analytic structure applies.

## Algorithm

```
1. Identify: A(ω) = response, F(ω) = perturbation, χ(ω) = susceptibility.
2. Causality: χ(t<0) = 0 → χ(ω) analytic for Im ω > 0.
3. Cauchy theorem on UHP contour → Kramers-Kronig:
   Re χ(ω) − χ(∞) = (2/π) P ∫₀^∞ u Im χ(u)/(u²−ω²) du
   Im χ(ω) = −(2ω/π) P ∫₀^∞ [Re χ(u)−χ(∞)]/(u²−ω²) du
4. ASYMMETRY (§82): Getting Re from Im is SAFE (any Im≥0 works).
   Getting Im from Re does NOT guarantee Im≥0.
5. Sum rules: high-ω expansion → integral constraints.
6. Fluctuation-dissipation: ⟨A²⟩_ω = ℏ coth(ℏω/2T) Im χ(ω) (quantum)
   or ⟨A²⟩_ω = (2T/ω) Im χ(ω) (classical).
```

## Instances: One Logic, Many Susceptibilities

| Volume | Context | χ(ω) | Response | Perturbation |
|--------|---------|------|----------|-------------|
| V5 §123 | Gen. susceptibility | α(ω) | ⟨x⟩ | Force f |
| V8 §77 | Dielectric | ε(ω)−1 | D | E |
| V8 §79 | Magnetic | μ(ω)−1 | B | H |
| V8 §82 | Conductivity | σ(ω) | j | E |
| V9 §76 | Quantum FDT | χ_AB(ω) | ⟨A⟩ | B |
| V9 §78 | Nyquist noise | iω/Z(ω) | J | ℰ |
| V10 §29 | Plasma dielectric | ε_l(k,ω)−1 | D | E |

## The Fluctuation-Dissipation Connection

Linear response theory is the bridge between TWO fundamental relations:
1. **Causality → Kramers-Kronig**: Re χ ↔ Im χ (dispersion relations)
2. **FDT**: Im χ ↔ spontaneous fluctuations (noise ↔ dissipation)

Together they mean: if you measure the noise spectrum of a system at
equilibrium, you know its complete linear response to ANY external
perturbation. This is among the deepest results in statistical physics.

## Key Properties

- Im χ(ω) > 0 for ω > 0 (dissipation, 2nd law)
- Re χ(ω) has NO sign constraint (can be positive or negative)
- χ(−ω) = χ*(ω) → Re χ even, Im χ odd
- For conductors: ω=0 pole → KK formulas modified (subtraction needed)
- Onsager: χ_AB(ω; H) = ε_A ε_B χ_BA(ω; −H)

## Cross-References

- Landau Vol.5 §122-125 (generalized susceptibility, classical FDT)
- Landau Vol.8 §77, §82 (ε(ω), Kramers-Kronig)
- Landau Vol.9 §75-78, §86-91 (quantum FDT, electromagnetic & hydrodynamic fluctuations)
- Landau Vol.10 §29 (plasma dielectric response)
- reasoning.causality_to_analyticity (specialization: ε(ω) derivation)
- reasoning.fluctuation_dissipation_quantum (specialization: quantum FDT)
- reasoning.spatial_dispersion (extension: χ(ω,k) nonlocal response)
