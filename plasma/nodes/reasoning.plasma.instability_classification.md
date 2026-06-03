---
skill_id: reasoning.plasma.instability_classification
type: reasoning
summary_50t: >
  Free energy source determines instability type. Configuration-space (fluid):
  ∇n, ∇T, ∇B, J → MHD instabilities (δW<0). Velocity-space (kinetic):
  non-Maxwellian f₀ → inverse Landau (∂f₀/∂v>0). Penrose criterion for
  absolute vs convective. Threshold and growth rate from D(k,ω)=0.
trigger:
  - plasma is observed to be unstable, need to identify mechanism
  - computing instability threshold and growth rate
reasoning_role: instability_taxonomy
parent: knowledge.kinetic.plasma_instabilities
retrieval_cost: 1
references:
  - landau-graph: knowledge.kinetic.plasma_instabilities
---

# reasoning.plasma.instability_classification — Free Energy → Growth

## Core Picture

All plasma instabilities draw free energy from either CONFIGURATION space
(gradients in real space) or VELOCITY space (non-Maxwellian distributions).

## Two Fundamental Classes

### Configuration-Space (Fluid/MHD) Instabilities

Free energy source: spatial gradients.

| Instability | Free energy | Condition | Example |
|------------|-------------|-----------|---------|
| Rayleigh-Taylor | ∇p opposite to g | Heavy fluid on top of light | Pellet ablation |
| Kelvin-Helmholtz | Velocity shear | v₁≠v₂ at interface | Magnetopause |
| Interchange/flute | ∇p·∇B < 0 (bad curvature) | δW < 0 | Tokamak edge, mirror |
| Kink (m=1) | Parallel current | q(a) < 1 (Kruskal-Shafranov) | Tokamak disruption |
| Sausage (m=0) | Azimuthal current | Any k, pinch | Z-pinch |
| Tearing | ∇J (current gradient) | Δ' > 0 | Island formation, sawteeth |
| Drift wave | ∇n₀ | Universal (always unstable) | Tokamak turbulence |

**Method**: Ideal MHD energy principle: δW < 0 ↔ unstable.
δW = (1/2)∫[|Q|²/μ₀ + γp|∇·ξ|² + (ξ·∇p)(κ·ξ) − 2(ξ·∇p)(ξ·κ) + ...] dV.

### Velocity-Space (Kinetic) Instabilities

Free energy source: ∂f₀/∂v > 0 somewhere.

| Instability | f₀ feature | Waves | Damping |
|------------|-----------|-------|---------|
| Bump-on-tail | ∂f₀/∂v > 0 at v_bump | Langmuir | Inverse Landau |
| Loss-cone | ∂f₀/∂v_⊥ > 0 | Whistler, ECM | Cyclotron maser |
| Temperature anisotropy | T_⊥ > T_∥ | Whistler, EMIC | Anisotropy-driven |
| Beam (two-stream) | Two cold beams | Electrostatic | Reactive (fluid) |
| Ion acoustic (current) | v_dr > c_s (electron drift) | Ion acoustic | Ion Landau competes |

**Method**: Penrose criterion — ∫ dv (∂f₀/∂v)/(v − ω/k) determines stability.
Nyquist analysis of D(k,ω) in complex ω-plane.

## Absolute vs Convective

- **Absolute** (ω complex, k real): grows in time at fixed position.
- **Convective** (ω real, k complex): grows in space, advected away.
- Determined by Green's function response to impulse (Briggs-Bers criterion).

## Cross-References

- Chen §6-7, Stix §10, Friedberg §8-9
- landau-graph: knowledge.kinetic.plasma_instabilities (kinetic types)
- landau-graph: reasoning.physical_solution_selection (Penrose ↔ causality)
