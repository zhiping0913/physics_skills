---
skill_id: reasoning.plasma.dielectric_tensor_magnetized
type: reasoning
summary_50t: >
  Magnetized cold plasma has anisotropic ε(ω): S (sum), D (difference), P (plasma).
  CMA diagram classifies all cold-plasma waves by ω_p²/ω² vs ω_c/ω.
  Cutoffs (k→0), resonances (k→∞), R/L/O/X wave taxonomy.
trigger:
  - EM wave propagation in magnetized plasma
  - need to classify wave modes and find accessibility windows
reasoning_role: magnetized_dielectric
parent: knowledge.kinetic.plasma_dielectric
retrieval_cost: 1
references:
  - landau-graph: knowledge.kinetic.plasma_dielectric
  - electrodynamics: knowledge.em.crystal_optics (analogy: anisotropic ε from B₀)
---

# reasoning.plasma.dielectric_tensor_magnetized — B₀ → Anisotropic ε(ω)

## Core Picture

A magnetic field B₀ breaks isotropy. In a COLD magnetized plasma with
B₀ = B₀ ẑ, the dielectric tensor is (Stix Ch.1-2, Ginzburg Ch.3):

```
        [ S   −iD   0  ]
ε(ω) =  [ iD    S   0  ]
        [ 0     0   P  ]
```

where the Stix parameters are:

```
S = ½(R+L)    R = 1 − Σ ω_pα²/[ω(ω+ω_cα)]    (right-hand cutoff)
D = ½(R−L)    L = 1 − Σ ω_pα²/[ω(ω−ω_cα)]    (left-hand cutoff)
P = 1 − Σ ω_pα²/ω²                             (plasma cutoff)
```

Sum over species α (electrons, ions). ω_cα = q_α B₀/m_α (signed).

## Algorithm: From ε to Wave Modes

```
1. Write wave equation: N×(N×E) + ε·E = 0, where N = ck/ω.

2. For angle θ between k and B₀, the dispersion determinant is:
   | S−N²cos²θ   −iD       N²sinθ cosθ |
   |    iD      S−N²        0          | = 0
   | N²sinθ cosθ  0      P−N²sin²θ    |

3. Expand → AN⁴ − BN² + C = 0, where:
   A = S sin²θ + P cos²θ
   B = RL sin²θ + PS(1+cos²θ)
   C = PRL

4. For each (ω,θ): solve quadratic for N² → two propagating modes.
```

## Wave Taxonomy (CMA Diagram)

**Parallel propagation (θ=0, k∥B₀):**
- R-wave (whistler/helicon): N² = R, RH circular, resonance at ω=ω_ce
- L-wave (ion cyclotron): N² = L, LH circular, resonance at ω=ω_ci

**Perpendicular propagation (θ=π/2, k⊥B₀):**
- O-mode (ordinary): N² = P, E∥B₀, unaffected by B₀, cutoff at ω=ω_p
- X-mode (extraordinary): N² = RL/S, E⊥B₀, cutoffs at R=0 (ω_R) and L=0 (ω_L),
  resonances at S=0 (upper/lower hybrid)

**CMA diagram**: Parameter space (ω_p²/ω², ω_c/ω) → each region has
different wave topology (number of propagating modes, resonance cones).

## Key Frequencies

| Frequency | Formula | Significance |
|-----------|---------|-------------|
| ω_p | √(n₀e²/ε₀m_e) | Plasma frequency — EM cutoff |
| ω_ce | eB₀/m_e | Electron cyclotron — R-wave resonance |
| ω_UH | √(ω_p²+ω_ce²) | Upper hybrid — X-mode resonance |
| ω_LH | √(ω_ci ω_ce) (approx) | Lower hybrid — ion dynamics |

## Cross-References

- Stix §1-2, Ginzburg §3-5, Chen §4
- landau-graph: knowledge.kinetic.plasma_dielectric (warm plasma ε)
- electrodynamics: knowledge.em.crystal_optics (same math, different physics)
