---
skill_id: reasoning.plasma.wave_kinetic_equation
type: reasoning
summary_50t: >
  ∂N_k/∂t + v_g·∇N_k − ∇ω_k·∇N_k = St[N_k]. Three-wave collision integral:
  St ∝ Σ |V_{k,k₁,k₂}|² [N₁N₂ − N_k(N₁+N₂)] δ(ω_k−ω₁−ω₂) δ(k−k₁−k₂).
  Manley-Rowe relations, Kolmogorov-Zakharov weak turbulence spectra.
  Wave action N_k = W_k/ω_k is the adiabatic invariant.
trigger:
  - computing nonlinear wave-wave energy transfer
  - saturation beyond quasilinear (mode coupling dominant)
reasoning_role: wave_kinetic_equation
parent: reasoning.plasma.quasilinear_diffusion
retrieval_cost: 1
---

# reasoning.plasma.wave_kinetic_equation — Waves as Quasiparticles

## Core Picture

When the wave spectrum is broad, nonlinear wave-wave interactions are
described by a kinetic equation for WAVE QUASIPARTICLES with occupation
number N_k = W_k/ω_k (wave action). The wave kinetic equation (WKE) is
the plasma-physics analog of the Boltzmann equation:

```
∂N_k/∂t + v_g·∇N_k − ∇ω_k·∇N_k = St_3[N_k] + St_4[N_k] + ...
```

The LEFT side is collisionless Liouville flow of wave packets. The RIGHT
side contains resonant three-wave (and four-wave) collision integrals
governing energy exchange between modes.

## Derivation Sketch

### 1. Wave action as adiabatic invariant

For narrow-band wave packets in slowly-varying media: N_k = W_k/ω_k is an
adiabatic invariant (Whitham 1965). In plasma:

```
W_k = ε₀ ∂(ω ε_h)/∂ω |E_k|²   [wave energy density, from ε(k,ω)]
N_k = W_k / ω_k                [wave action — conserved in geometric optics]
```

The left-hand side ∂N_k/∂t + v_g·∇N_k − ∇ω_k·∇N_k = 0 is IDENTICAL to
the collisionless Boltzmann equation with ω_k as the effective Hamiltonian.

### 2. Three-wave collision integral

Three waves satisfying the resonance conditions exchange energy coherently:

```
ω_k = ω_{k₁} + ω_{k₂}     [frequency matching]
k = k₁ + k₂               [wavevector matching]
```

The collision integral is:

```
St_3[N_k] = π Σ_{k₁,k₂} |V_{k,k₁,k₂}|² { N_{k₁}N_{k₂} − N_k(N_{k₁}+N_{k₂}) }
            × δ(ω_k−ω_{k₁}−ω_{k₂}) δ(k−k₁−k₂)
```

The coupling coefficient V comes from quadratic nonlinearity in the plasma
equations. For key processes:

| Process | |V|² scaling |
|---------|------------|
| L → L' + IA (Langmuir decay) | ∝ ω_p (kλ_D)² |
| IA → IA' + IA | ∝ ω_{pi} |
| A → A' + MS (Alfvén decay) | ∝ ω_{ci} |

### 3. Manley-Rowe relations

Three-wave coupling conserves wave action in the sense of quantum energy
partitioning: ΔN_k/ω_k = ΔN_{k₁}/ω_{k₁} = −ΔN_{k₂}/ω_{k₂}. One pump
quantum (ℏω_k) → one quantum each of daughter waves (ℏω₁ + ℏω₂).

### 4. Kolmogorov-Zakharov spectra

For scale-invariant couplings (ω ∝ k^α), steady-state flux solutions:

```
N_k ∝ k^{−α−d−m}        [direct energy cascade to small scales]
N_k ∝ k^{−α−d−m+β}      [inverse cascade to large scales]
```

These are the wave-turbulence analogs of Kolmogorov E(k) ∝ k^(−5/3).

## Algorithm — Decay product spectrum from pump

```
1. Identify pump: ω₀, k₀.
2. Find ALL resonant triads (ω₀,k₀) = (ω₁,k₁) + (ω₂,k₂) where daughters
   satisfy their linear dispersion relations.
3. Compute matrix element V from fluid or kinetic nonlinearity.
4. Parametric instability: linearize N₁, N₂ ≪ N₀ → γ₀ = |V|²N₀/(∂ω₁/∂N₁).
5. Steady turbulence: solve St_3[N_k]=0 → KZ spectrum.
```

## Edge Cases

- **Four-wave regime**: when three-wave resonance is impossible (e.g.,
  Langmuir: ω(k) > ω(k₁)+ω(k₂) for all k₁,k₂), the leading nonlinearity
  is four-wave → St_4 ∝ |T|²∫N₁N₂N₃… This leads to NLS in the narrow-band
  limit (see `mt.soliton_formation`).
- **Strong turbulence**: N_k k^d > 1 → random-phase approximation breaks.
  Phase-correlated dynamics require Zakharov equations.

## Cross-References

- Zakharov, L'vov, Falkovich, *Kolmogorov Spectra of Turbulence* (1992)
- Kadomtsev, *Plasma Turbulence* (1965)
- plasma: reasoning.plasma.quasilinear_diffusion (parent — particle diffusion)
- plasma: reasoning.plasma.instability_classification (linear ↦ decay)
- mathematics-theorems: mt.soliton_formation (NLS for four-wave regime)
- electrodynamics: reasoning.em.three_wave_parametric_coupling (same math in optics)
