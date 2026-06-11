---
skill_id: reasoning.plasma.quasilinear_diffusion
type: reasoning
summary_50t: >
  ∂f₀/∂t = (∂/∂v)[D_QL(v) ∂f₀/∂v] with D_QL ∝ Σ_k |E_k|² δ(ω_k−kv).
  Plateau formation when ∂f₀/∂v=0 in resonance region. Wave energy evolution
  ∂W_k/∂t = 2γ_k W_k with γ_k from linear theory using time-dependent f₀.
  Vedenov-Velikhov-Sagdeev quasilinear theory (1961-62).
trigger:
  - computing saturation of kinetic instability
  - estimating velocity-space diffusion from wave spectrum
reasoning_role: quasilinear_diffusion
parent: reasoning.plasma.wave_particle_resonance
retrieval_cost: 1
---

# reasoning.plasma.quasilinear_diffusion — Waves → Velocity-Space Diffusion

## Core Picture

When a kinetic instability saturates, the unstable waves react back on the
particle distribution f₀(v) via resonant wave-particle interaction. The
quasilinear theory closes the coupled wave-particle system by averaging
over the fast oscillation period:

```
∂f₀/∂t = (∂/∂v)[D_QL(v, t) ∂f₀/∂v]     [diffusion in velocity space]
∂W_k/∂t = 2 γ_k[f₀(t)] W_k             [wave energy evolution]
```

The key insight: D_QL is PROPORTIONAL to W_k — the wave energy that the
waves deposit into the particles. This creates a self-consistent feedback
loop: waves grow (γ>0) → D_QL diffuses f₀ → flattening reduces γ → saturation.

## Derivation Sketch

### 1. Decomposition and averaging

Write f = f₀(v, t) + δf(x, v, t). f₀ evolves SLOWLY (diffusion time
∼ γ⁻¹(v_th/v_tr)² ≫ γ⁻¹). δf oscillates at ω_p. Linearize:

```
∂δf/∂t + v·∇δf + (q/m)E·∂f₀/∂v = 0
```

Fourier: δf_k(v,t) with E_k(t) ∝ exp(−iω_k t + γ_k t).

### 2. Slow evolution from nonlinear feedback

The ensemble-averaged quadratic term feeds back on f₀:

```
∂f₀/∂t = −(q/m) ∂/∂v · ⟨δf δE⟩
```

where ⟨·⟩ = average over fast oscillation and random phases.

### 3. Quasilinear diffusion coefficient

Substituting the linear solution for δf_k and using the resonance condition
ω_k ≈ k v (Landau resonance), the diffusion coefficient emerges:

```
D_QL(v) = (2π² q²/m²) ∫ dk |E_k|² δ(ω_k − k v)   [1D electrostatic]
```

In magnetized plasma: ω − k_∥ v_∥ − n ω_c = 0 → diffusion in both v_∥ and v_⟂.
For electromagnetic waves: D_QL acquires a tensor structure coupling different
velocity components.

### 4. Plateau formation

Steady state (∂f₀/∂t = 0) requires D_QL ∂f₀/∂v = 0 wherever D_QL > 0.
For a monochromatic wave: D_QL(v) nonzero only near v_res = ω/k → a FLAT
PLATEAU forms centered at v_res. Total resonant-particle number and energy
are conserved during plateau formation.

### 5. Wave saturation

The wave energy evolves: dW_k/dt = 2γ_k[f₀(t)] W_k where γ_k is computed
from linear theory using the TIME-DEPENDENT f₀. Saturation occurs when the
plateau eliminates ∂f₀/∂v > 0 (no more free energy).

## Algorithm — Instability saturation estimate

```
1. Identify unstable mode: ω, γ_L (linear growth rate), k
2. Estimate saturation energy: W_sat ∼ (γ_L/ω_p) n k_B T_e (Manheimer rule)
3. Compute D_QL(v) from W_sat
4. Solve ∂f₀/∂t = ∂_v(D_QL ∂_v f₀) → plateau width Δv ∼ (2D_QL/γ_L)^(1/2)
5. Plateau flattens ∂f₀/∂v=0 → instability quenched → consistent
```

## Edge Cases

- **Inhomogeneous plasma**: spatial gradients add convection → ∂f₀/∂t + v ∂f₀/∂x = ∂_v(D_QL ∂_v f₀). Plateau may be spatially localized.
- **Trapped particle regime**: when bounce frequency ω_B = k√(eφ/m) > γ_L, trapping dominates over quasilinear diffusion. Transition at eφ/k_B T_e ∼ (γ_L/ω_B)².
- **Strong turbulence breakdown**: W/nT ≳ (kλ_D)² → mode coupling (three-wave, four-wave) competes with quasilinear. See `reasoning.plasma.wave_kinetic_equation`.

## Cross-References

- Vedenov, Velikhov & Sagdeev, Nucl. Fusion 1, 82 (1961); Usp. Fiz. Nauk 73, 701 (1961)
- Kadomtsev, *Plasma Turbulence* (1965), Ch.2
- plasma: reasoning.plasma.wave_particle_resonance (parent)
- plasma: reasoning.plasma.wave_kinetic_equation (next hierarchy level)
- plasma: reasoning.plasma.instability_classification (unstable mode identification)
