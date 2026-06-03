---
skill_id: reasoning.optics.laser_rate_equations
type: reasoning
summary_50t: >
  dN₂/dt = R_p − N₂/τ − σ(N₂−N₁)I/hν. Threshold N_th, gain g=g₀/(1+I/I_sat).
  Steady-state: P_out = η(P_pump−P_th). Q-switch: store energy→dump→giant pulse.
  Mode locking: φ_n−φ_{n−1}=const → τ_p∼1/Δν. CPA: stretch→amplify→compress.
trigger:
  - designing laser oscillator/amplifier, computing output power
  - Q-switched or mode-locked pulse generation
reasoning_role: laser_dynamics
parent: reasoning.equilibrium_as_extremum
retrieval_cost: 1
references:
  - landau-graph: reasoning.equilibrium_as_extremum (steady-state = pump-loss balance)
---

# reasoning.optics.laser_rate_equations — Pump → Gain → Coherent Output

## Core Picture

A laser is an optical oscillator: gain medium provides amplification, cavity
provides feedback. The dynamics are captured by coupled rate equations for
the population inversion ΔN = N₂−N₁ and the intracavity photon density φ
(Siegman §6-7, §12-13; Svelto §7-8).

## Algorithm

```
1. RATE EQUATIONS (4-level laser, homogeneously broadened):
   dΔN/dt = R_p − ΔN/τ − (σ c/η) ΔN φ
   dφ/dt   = (σ c/η) ΔN φ − φ/τ_c + β ΔN/τ
   where: R_p = pump rate, τ = upper-state lifetime, σ = stimulated
   emission cross-section, τ_c = cold cavity photon lifetime.

2. THRESHOLD: steady-state d/dt=0, φ→0.
   ΔN_th = η/(σ c τ_c). R_p,th = ΔN_th/τ.
   Threshold pump power: P_th = hν_p R_p,th V_mode.

3. STEADY-STATE ABOVE THRESHOLD:
   ΔN = ΔN_th (clamped at threshold).
   φ = (τ_c/hν)[P_pump − P_th].
   Output: P_out = T φ hν A_beam = η_slope (P_pump − P_th).

4. GAIN SATURATION (Siegman §7):
   g(I) = g₀ / (1 + I/I_sat).
   I_sat = hν/(σ τ) for 4-level systems.

5. RELAXATION OSCILLATIONS: small perturbation around steady-state →
   damped oscillation at ω_rel ≈ √[(σc/η)φ/τ] ∼ 10⁵−10⁶ rad/s.
```

## Q-Switching (Siegman §24, Svelto §8)

```
1. Hold cavity at low Q (shutter closed) → pump stores energy in gain medium.
2. Suddenly switch to high Q → φ builds from noise → ΔN depleted.
3. Giant pulse: P_peak ≈ (hν/τ_c) ΔN_i V, τ_pulse ∼ τ_c.
   Energy: E_out ≈ (ΔN_i−ΔN_f) hν V ≈ η_ext E_stored.
```

## Mode Locking (Siegman §27, Svelto §8)

N longitudinal modes with fixed phase relation φ_n−φ_{n−1} = const → periodic
pulse train. τ_p ≈ 1/Δν (transform limit). f_rep = c/2L.
Active: AM/FM modulator at f_rep. Passive: saturable absorber (fast: SESAM, slow: dye).
KLM: Kerr lens from n₂(I) → self-focusing → higher gain for pulsed mode.

## CPA (Chirped Pulse Amplification, Nobel 2018)

Stretch (τ→ns) → amplify (avoid damage) → compress (τ→fs). Grating pair
provides positive/negative GDD. P_peak increased by 10³−10⁵×.

## Cross-References

- Siegman §6-7, §12-13, §24, §27; Svelto §7-8
- landau-graph: reasoning.equilibrium_as_extremum (steady-state balance)
- landau-graph: reasoning.normal_mode_decomposition (N cavity modes)
