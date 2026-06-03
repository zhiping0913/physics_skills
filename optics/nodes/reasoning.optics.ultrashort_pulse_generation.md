---
skill_id: reasoning.optics.ultrashort_pulse_generation
type: reasoning
summary_50t: >
  Mode locking: N modes, φ_{n}−φ_{n−1}=const → τ_p∼1/Δν, f_rep=c/2L.
  Active (AM/FM) or passive (SESAM, KLM). KLM: Kerr lens self-focusing→
  effective fast saturable absorber. CPA: stretch→amplify→compress.
  Few-cycle: octave-spanning→f_{CEO} control→attosecond.
trigger:
  - designing femtosecond/attosecond laser systems
  - generating transform-limited ultrashort pulses
reasoning_role: pulse_generation
parent: reasoning.optics.laser_rate_equations
retrieval_cost: 1
---

# reasoning.optics.ultrashort_pulse_generation — Phase Lock → τ_p ∼ 1/Δν

## Core Picture

A laser cavity supports N longitudinal modes at frequencies ν_n = n·c/2L.
In normal (free-running) operation, each mode has random phase. If we FORCE
all modes to have a fixed phase relationship φ_n − φ_{n−1} = const, the
output becomes a periodic train of ultrashort pulses (Siegman §27, Svelto §8).

## Algorithm: Mode-Locked Pulse

```
1. N modes, equal amplitude E₀, fixed phase difference Δφ:
   E(t) = Σ_{n=0}^{N−1} E₀ exp[i(ω₀+nΔω)t + inΔφ]
        = E₀ exp(iω₀t) sin(NΔω t/2)/sin(Δω t/2)
   where Δω = 2π·c/2L.

2. Pulse duration: τ_p ≈ 1/(N Δν) = 1/Δν_gain (transform limit).
   For Gaussian: τ_p Δν = 0.44. For sech²: τ_p Δν = 0.315.

3. Repetition rate: f_rep = c/2L. Pulse energy: E_pulse = P_avg/f_rep.
   Peak power: P_peak ≈ E_pulse/τ_p ∼ P_avg × (Δν_gain/f_rep).

4. Nuance: Δφ = 0 gives maximum at t=0 (AM mode locking).
   Δφ = π gives alternating sign (FM mode locking, broader spectrum).
```

## Mode-Locking Methods

**Active**: AM modulator at f_rep (acousto-optic or electro-optic).
Loss modulation → only the pulse that arrives when loss is minimum survives.
Pulse duration limited by modulator bandwidth: τ_p ∼ 1/(f_rep Δν_mod).

**Passive (saturable absorber)**:
SESAM (semiconductor saturable absorber mirror): fast recovery (ps-fs).
Dye: slow recovery — but combined with gain saturation → effective fast response.
No electronics needed — self-starting.

**Kerr lens mode locking (KLM)**: (Siegman §27.4)
n₂ > 0 → self-focusing → higher intensity on axis in gain medium →
hard aperture (or soft aperture from pump-gain overlap) → lower loss for
pulsed (high peak power) vs CW operation. Effective fast saturable absorber.

## CPA (Chirped Pulse Amplification)

Stretch (grating pair, positive GDD, ps→ns) → amplify (fiber or regenerative,
avoid damage) → compress (grating pair, negative GDD, ns→fs).
Stretcher-compressor must be matched in GDD and higher-order dispersion.
Treacy (grating) compressor; Martinez (grating+lens) stretcher.

## Cross-References

- Siegman §27, Svelto §8, Trebino §1-3
- landau-graph: reasoning.normal_mode_decomposition (N cavity modes)
