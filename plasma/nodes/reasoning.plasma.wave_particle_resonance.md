---
skill_id: reasoning.plasma.wave_particle_resonance
type: reasoning
summary_50t: >
  ω−k_∥v_∥ = nω_c selects resonant particles that stay in phase with wave.
  n=0: Landau damping (electrostatic) + transit-time (magnetic). n=±1: cyclotron.
  |n|≥2: Bernstein (undamped). Quasilinear diffusion: ∂f₀/∂t = ∂/∂v(D_QL ∂f₀/∂v).
trigger:
  - computing wave damping/growth from particle distribution
  - need resonant velocity condition for specific harmonic
  - quasilinear evolution of distribution function
reasoning_role: resonance_condition
parent: reasoning.landau_damping
retrieval_cost: 1
references:
  - landau-graph: reasoning.landau_damping (n=0 electrostatic case)
---

# reasoning.plasma.wave_particle_resonance — Phase Matching → Energy Exchange

## Core Picture

Wave-particle interaction occurs when a particle sees a STATIONARY wave phase
in its own reference frame. The general resonance condition for a magnetized
plasma (Stix §8-9, Chen §7, Ginzburg §6):

```
ω − k_∥ v_∥ = n ω_c    (n = 0, ±1, ±2, ...)
```

where ω_c = qB₀/m is the (signed) cyclotron frequency. Each n selects a
different harmonic of the cyclotron motion.

## Algorithm

```
1. Write wave fields in particle's guiding-center frame:
   E(t) = Σ E_n exp[i(k_∥ z_∥ + k_⊥ r_L sin θ − ωt)]

2. Expand in Bessel functions: exp(ik_⊥ r_L sin θ) = Σ J_m(k_⊥ r_L) e^{imθ}

3. The particle sees frequency-shifted components at ω' = ω − k_∥ v_∥ − m ω_c.
   Resonance: ω' = 0 → ω − k_∥ v_∥ = n ω_c.

4. Resonant particles EXCHANGE energy with the wave:
   - ∂f₀/∂v|_{v_res} < 0 → LANDAU DAMPING (energy from wave to particles)
   - ∂f₀/∂v|_{v_res} > 0 → INVERSE DAMPING / INSTABILITY (bump-on-tail)

5. For n=0 (Landau, transit-time): parallel dynamics, no B₀ needed.
   For n=±1 (cyclotron): perpendicular dynamics, needs B₀.
   For |n|≥2 (Bernstein): finite Larmor radius, K⊥ρ_L ∼ n, undamped.
```

## Resonance Types

| n | Name | Physics | Damping mechanism |
|---|------|---------|-------------------|
| 0 | Landau | Electrostatic, E_∥ | Parallel trapping, phase mixing |
| 0 | Transit-time | Magnetic, μ∇B force | Mirror force on magnetic moment |
| ±1 | Cyclotron | E_⊥ rotates with particle | Perpendicular heating |
| ±2,... | Bernstein | Finite Larmor radius | Undamped! (k_∥ → 0) |

## Quasilinear Theory (Stix §10, Chen §8)

Beyond linear damping: the wave spectrum modifies f₀(v) via diffusion:

```
∂f₀/∂t = ∂/∂v_∥ (D_∥ ∂f₀/∂v_∥) + (1/v_⊥)∂/∂v_⊥ (v_⊥ D_⊥ ∂f₀/∂v_⊥)
D ∝ Σ |E_k|² δ(ω_k − k_∥ v_∥ − n ω_c)
```

This flattens f₀ near resonance → saturation of instability → plateau formation.

## Cross-References

- Stix §8-10, Chen §7-8, Ginzburg §6-7
- landau-graph: reasoning.landau_damping (n=0 electrostatic)
- landau-graph: reasoning.plasma_dielectric_response (ε_l from Vlasov)
