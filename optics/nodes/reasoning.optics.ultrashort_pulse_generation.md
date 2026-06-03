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
sign_convention: >
  Time-bandwidth product: Gaussian τ_p Δν = 0.44 (FWHM, field).
  sech² τ_p Δν = 0.315. Δφ = 0: AM mode-locking (all modes in phase at t=0).
  Δφ = π: FM mode-locking. f_rep = c/2L = free spectral range.
  Positive chirp = red leads blue (longer λ arrives earlier). CEP φ_CEO = φ_carrier − φ_envelope.
---

# reasoning.optics.ultrashort_pulse_generation — Phase Lock → τ_p ∼ 1/Δν

## Core Picture

A laser cavity supports N longitudinal modes at frequencies ν_n = n·c/2L.
In normal (free-running) operation, each mode has random phase. If we FORCE
all modes to have a fixed phase relationship φ_n − φ_{n−1} = const, the
output becomes a periodic train of ultrashort pulses (Siegman §27, Svelto §8).

## Derivation Sketch

Starting from `optics: reasoning.optics.laser_rate_equations` (rate equations
establish that N longitudinal modes can oscillate simultaneously once above
threshold; without phase locking, these are independent — the laser output
is CW with random amplitude fluctuations):

1. **Mode-locking as interference** (the key insight — Siegman §27.2):
   N modes with equal amplitude E₀ and fixed phase difference Δφ. Summation:
   ```
   E(t) = Σ_{n=0}^{N−1} E₀ exp[i(ω₀ + nΔω)t + inΔφ]
        = E₀ exp(iω₀t) · sin(N Δω t/2) / sin(Δω t/2)
        = E₀ exp(iω₀t) · N · sinc(N Δω t/2π)  (for Δφ=0, large N)
   ```
   This is periodic with T = 2π/Δω = 2L/c (cavity round-trip time). The
   constructive interference occurs at t = 0, T, 2T, ... giving a pulse
   train. The CRITICAL NON-OBVIOUS step: the sum of equally-spaced frequency
   components is a Dirac COMB — the mode-locked laser is a temporal
   frequency comb in the time domain, dual to the frequency comb in the
   spectral domain (which became the 2005 Nobel prize, Hänsch & Hall).

2. **Consuming parent edge**: The rate equations (laser_rate_equations) provide
   the gain dynamics that determine HOW MANY modes oscillate (N = Δν_gain / Δν_FSR)
   and under what conditions they can coexist. But rate equations alone
   have NO phase information (they track photon number, not field phase).
   Mode locking REQUIRES an additional mechanism that couples adjacent
   modes' phases. This is the conceptual gap this node bridges.

3. **Time-bandwidth product** (transform limit — the fundamental constraint):
   The achievable pulse duration is set by the gain bandwidth:
   ```
   Gaussian pulse shape:  τ_p · Δν = 0.441 (FWHM, field)
   sech² pulse shape:     τ_p · Δν = 0.315
   Lorentzian:            τ_p · Δν = 0.221
   Rectangular spectrum:  τ_p · Δν = 0.886
   ```
   The product is a SHAPE-DEPENDENT constant. Ti:Sapphire with Δν ≈ 128 THz
   (Δλ ≈ 300 nm at 800 nm) supports τ_p ≈ 3.4 fs (sech²). The measured
   TBP > transform limit indicates CHIRP (residual GDD). The TBP is a
   diagnostic: if you measure τ_p and Δν, the ratio tells you whether
   the pulse is transform-limited or chirped.

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

**Soliton mode-locking** (Kartner §4, Agrawal §5):
In the anomalous GVD regime (β₂ < 0), the NLSE balance between GVD broadening
and SPM narrowing produces a fundamental soliton: N² = γ P₀ τ₀² / |β₂| = 1.
The soliton is a STABLE attractor — perturbations (from gain, loss, filtering)
are continuously corrected by the soliton's self-healing property. In
soliton mode-locked fiber lasers, the pulse shape is intrinsically sech²
(not Gaussian), and the TBP is exactly 0.315. The pulse energy is limited
by the soliton area theorem (E_soliton ∝ |β₂|/τ); higher energy causes
wave-breaking → multiple solitons. Consumes `optics: reasoning.optics.pulse_propagation_nlse`
for the NLSE framework (bidirectional: ultrashort_pulse uses NLSE soliton
physics; NLSE's soliton section cites mode-locked lasers as the application).

**Stretched-pulse / dispersion-managed soliton**: Alternating normal and
anomalous GVD segments → pulse breathes (stretches/compresses per round trip)
→ reduces average nonlinear phase → supports 10-100× higher energy than
soliton mode-locking. Net cavity GDD ≈ 0 (slightly anomalous for self-starting).

## CPA (Chirped Pulse Amplification)

Stretch (grating pair, positive GDD, ps→ns) → amplify (fiber or regenerative,
avoid damage) → compress (grating pair, negative GDD, ns→fs).
Stretcher-compressor must be matched in GDD and higher-order dispersion.
Treacy (grating) compressor; Martinez (grating+lens) stretcher.

**Gain narrowing in CPA** (critical limitation): The gain medium has a finite
bandwidth Δν_gain. After amplification, the effective spectral bandwidth shrinks:
```
Δν_out ≈ Δν_in / √(1 + ln G · (Δν_in/Δν_gain)²)
```
For Ti:Sapphire (Δν_gain ≈ 128 THz) with G = 10⁶ and Δν_in = 100 THz,
Δν_out ≈ 35 THz (τ_p ~ 13 fs vs. input 4.4 fs). Mitigation: regenerative
pulse shaping (acousto-optic or liquid-crystal spectral amplitude filter
placed inside the regenerative amplifier cavity, counteracting the gain
profile), or OPCPA (optical parametric CPA using BBO/LBO — parametric
bandwidth can exceed 200 THz for few-cycle pulses).

## CEP Stabilization (Few-Cycle Pulses)

For pulses with τ_p < 2 optical cycles, the carrier-envelope phase (CEP)
φ_CEO = φ_carrier − φ_envelope matters — the electric field under the envelope
shifts from pulse to pulse. CEP drift per round trip:
```
Δφ_CEO = (2πL/c) · (v_g − v_φ) / (v_g v_φ) · ω₀ = 2π · f_CEO / f_rep
```
where f_CEO = f_rep · Δφ_CEO/(2π) is the carrier-envelope offset frequency.

**Measurement: f-2f interferometry** (Hänsch 1999): An octave-spanning
spectrum (e.g., from photonic crystal fiber broadening) provides frequency
components at f_n = n·f_rep + f_CEO. Frequency-double the n-th comb line:
2f_n = 2n·f_rep + 2f_CEO. Beat it with the 2n-th line: f_{2n} = 2n·f_rep + f_CEO.
The beat note: 2f_n − f_{2n} = f_CEO. Lock this beat to a stable RF reference
by feedback to pump power (changes group velocity) or cavity length (changes f_rep).

**Stabilization methods**:
- **Pump power modulation**: changes v_g via intensity-dependent nonlinear
  index → adjusts Δφ_CEO. Bandwidth ~ few kHz.
- **AOM in pump beam** (acousto-optic modulator): faster than pump current,
  bandwidth ~ 100 kHz.
- **Feed-forward** (Koke 2010): measure Δφ_CEO on every pulse via fast detector
  + electronics, apply compensating phase shift via AOM in the output beam.
  No feedback loop → no servo bandwidth limitation. Enables single-shot
  CEP control at full repetition rate. Reference: Koke et al., Nature Photon.
  4, 462 (2010).

## Edge Cases

- **Q-switching instability in mode-locked lasers** (Siegman §27.5): If
  the saturable absorber recovery time is too slow relative to the cavity
  lifetime, relaxation oscillations can drive the laser into Q-switched
  mode-locking (bursts of mode-locked pulses under a Q-switch envelope).
  Unstable for most applications. Criterion: E_pulse > E_sat,gain · E_sat,abs / (E_sat,gain + E_sat,abs) to suppress.
  Switch to SESAM with faster recovery or higher modulation depth.
- **Few-cycle pulses (< 5 fs)**: dispersion compensation must extend to
  higher orders (TOD, FOD). Need double-chirped mirrors (DCMs, Kärtner) or
  combination of chirped mirrors + adaptive pulse shaper (4-f SLM). 
  Octave-spanning spectra require all-reflective optics (metal-coated or
  DCM-only) — transmissive optics introduce GDD that cannot be compensated
  over an octave. Material dispersion control: minimize glass path (thin
  output coupler wedges, no Brewster plates).
- **Thermal effects at high average power**: In high-repetition-rate (> 10 MHz)
  CPA systems, the average power heats the gain medium, causing thermal
  lensing and stress birefringence. For > 100 W average, switch to
  cryogenically cooled Yb:YAG thin-disk or Innoslab geometry for better
  heat extraction.

## Cross-References

- Siegman §27, Svelto §8, Trebino §1-3
- landau-graph: reasoning.normal_mode_decomposition (N cavity modes)
- optics: reasoning.optics.laser_rate_equations (parent edge: Derivation Sketch
  step 2 explicitly consumes gain dynamics to determine number of oscillating
  modes; bidirectional — ultrashort_pulse is the phase-locked extension of
  rate-equation dynamics)
- optics: reasoning.optics.pulse_propagation_nlse (soliton mode-locking: the
  NLSE balance GVD/SPM produces soliton pulses in fiber lasers. Bidirectional:
  NLSE provides soliton physics; this node provides the mode-locking context)
