---
skill_id: reasoning.uo.mode_locking_active
type: reasoning
summary_50t: >
  Active mode-locking: periodic modulation of cavity loss (AM) or phase (FM)
  at f_mod = f_rep = c/2L. AM: Gaussian pulse τ_p ∝ 1/√(f_m Δν_g).
  FM: frequency-swept pulse, chirped output. Küpfmüller transient:
  N ∼ √(Δν_g/f_m) modes needed to reach steady-state. Pulse width limited
  by gain bandwidth Δν_g via τ_p ≈ 0.44/Δν_g (AM) or τ_p ≈ 0.63/Δν_g (FM).
trigger:
  - analyzing AM or FM mode-locked laser dynamics
  - computing steady-state pulse width from modulation parameters
  - understanding pulse formation transient (build-up from noise)
reasoning_role: active_mode_locking
parent: reasoning.optics.laser_rate_equations
retrieval_cost: 1
sign_convention: >
  AM modulation depth M = ΔT_mod/T_cav (fractional loss modulation).
  FM modulation index δ_c = Δω_m/ω_m (peak phase deviation).
  Modulation frequency f_m = c/2L (fundamental) or N·c/2L (harmonic).
  τ_p = FWHM of intensity.
references:
  - optics: reasoning.optics.laser_rate_equations (parent — laser dynamics)
---

# reasoning.uo.mode_locking_active — Periodic Modulation → Fixed-Phase Mode Train

## Core Picture

Active mode-locking imposes a periodic time-varying loss (AM) or phase (FM)
inside the laser cavity at a frequency exactly equal to the cavity round-trip
frequency f_rep = c/2L. This periodic modulation forces all oscillating
longitudinal modes to acquire a fixed phase relationship, producing a train
of ultrashort pulses. The steady-state pulse is typically Gaussian (AM) or
chirped Gaussian (FM), with duration limited by the gain bandwidth (Weiner §2,
Siegman §27.1-27.4, Svelto §8).

## Derivation Sketch

### 1. Modulation as mode-coupling

Consider N longitudinal modes at frequencies ν_n = n·c/2L. An intracavity
AM modulator driven at f_m = c/2L sinusoidally modulates the loss:
```
loss(t) = loss₀ [1 − M cos(2π f_m t)]
```
where M is the modulation depth. Each mode develops sidebands at ν_n ± f_m
that injection-lock adjacent modes → all mode phases become correlated.

### 2. Steady-state AM mode-locking (Weiner §2.1)

In the frequency domain, the circulating pulse spectrum A(ω) satisfies the
self-consistency condition: after one round-trip through gain, loss, modulator,
and filter, the pulse reproduces itself. For Gaussian filter bandwidth Δν_g
(FWHM of gain) and sinusoidal AM modulation:

**Steady-state pulse** (Gaussian shape):
```
|a(t)|² ∝ exp[−2t²/τ_p²]
τ_p = √(2√2 ln 2 / π) · √(1/(f_m Δν_g)) · M^{-1/4}
    ≈ 0.45 · √(1/(f_m Δν_g)) · M^{-1/4}
```

**Küpfmüller transient**: Starting from noise, the number of round-trips to
reach steady-state is:
```
N_ss ≈ √(Δν_g / f_m)
```
Each round-trip, the modulator sidebands couple ±1 mode. After N round-trips,
∼2N modes are phase-locked. Saturation when all modes within Δν_g are locked.

**Bandwidth-limited minimum**: For strong modulation (M ∼ 0.5) and broad gain:
```
τ_p,min ≈ 0.44 / Δν_g    (transform-limited Gaussian)
```
Example: Ti:sapphire (Δν_g ≈ 100 THz) → τ_p,min ≈ 4.4 fs (AM mode-locking
limit). In practice, active mode-locking achieves ∼1-10 ps due to limited
modulator bandwidth (f_m ≪ Δν_g).

### 3. FM mode-locking (Weiner §2.2)

An intracavity phase modulator driven at f_m = c/2L produces:
```
FM: φ(t) = δ_c cos(2π f_m t)
     → E_out(t) = E_in(t) · exp[iδ_c cos(2π f_m t)]
```
where δ_c is the modulation index (peak phase deviation).

**Steady-state pulse**: Chirped Gaussian with:
```
τ_p ≈ 0.63 / √(δ_c f_m Δν_g)    (chirped; broader than AM)
```
FM mode-locked pulses are inherently chirped and require external compression.

**Key difference from AM**: FM mode-locking produces two independent
steady-state pulse trains shifted by half a period — spontaneous
bistability. An intracavity etalon or saturable absorber selects one.

### 4. Detuning sensitivity

The modulation frequency must MATCH the cavity round-trip frequency:
```
f_m = c/2L    (exact, or integer multiple for harmonic ML)
```
Detuning Δf = f_m − f_rep causes pulse timing jitter and eventual
loss of mode-locking. Tolerance: Δf/f_rep ≲ 10⁻⁵ for stable operation.

### 5. Harmonic mode-locking

Driving the modulator at f_m = N·c/2L (N-th harmonic) produces N equally
spaced pulses per round-trip. Requires suppression of supermode competition
via intracavity etalon or gain saturation. Used in fiber lasers for
high-repetition-rate sources (10-100 GHz).

## Algorithm — Given Laser Parameters → ML Pulse

```
1. INPUT: cavity length L, gain bandwidth Δν_g (FWHM), modulation depth M
   or modulation index δ_c, round-trip loss ℓ₀, small-signal gain g₀.

2. CHECK stability: f_m = c/2L within 10⁻⁵ tolerance. Q-switching
   suppression: g₀/ℓ₀ < threshold (∼1.2-1.5 for stable CW-ML).

3. COMPUTE steady-state pulse (AM):
   τ_p ≈ 0.45 · √(1/(f_m Δν_g)) · M^{-1/4}
   Check: τ_p Δν_g ≥ 0.44 (transform limit for Gaussian).
   If computed τ_p < 0.44/Δν_g → set τ_p = 0.44/Δν_g (bandwidth-limited).

4. For FM mode-locking:
   τ_p ≈ 0.63 / √(δ_c f_m Δν_g)
   Pulse is chirped; bandwidth ≈ √(δ_c f_m Δν_g).

5. ESTIMATE transient: N_ss ≈ √(Δν_g/f_m) round-trips.
   Build-up time ≈ N_ss · 2L/c.

6. COMPUTE average power and peak power from CW power and duty cycle.
```

## Edge Cases

- **Regenerative mode-locking**: Feedback loop actively stabilizes f_m to
  the detected f_rep. Cancels detuning. Common in fiber lasers.
- **AM-FM coupling**: Real modulators have both AM and FM components.
  AM component dominates pulse formation; FM adds chirp.
- **Super-mode competition** in harmonic ML: noise in the inter-pulse
  spacing → need supermode suppression filter or saturable absorber.
- **Q-switching instability**: Excessive pump power causes relaxation
  oscillations that kill mode-locking. Stay below Q-switching threshold.

## Cross-References

- Weiner §2.1-2.3; Siegman §27.1-27.4; Svelto §8.5
- optics: reasoning.optics.laser_rate_equations (parent — laser dynamics,
  gain saturation)
- ultrafast-optics: reasoning.uo.mode_locking_passive (sibling — alternative
  ML mechanism using nonlinearity instead of external modulation)
- ultrafast-optics: reasoning.uo.pulse_propagation_linear (output pulse
  propagation through dispersive elements)
