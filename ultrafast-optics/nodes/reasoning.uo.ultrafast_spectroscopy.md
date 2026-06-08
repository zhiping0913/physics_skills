---
skill_id: reasoning.uo.ultrafast_spectroscopy
type: reasoning
summary_50t: >
  Pump-probe: Δt delay → ΔT(t) transient absorption/reflection. Photon echo:
  two pulses (τ) + third at T → echo at 2τ+T, decay ∝ exp(−2T/T₂) gives
  T₂ dephasing. 2D spectroscopy: three pulses → rephasing (k_I=−k₁+k₂+k₃)
  and non-rephasing (k_II=+k₁−k₂+k₃) signals → 2D correlation map
  (ω_excitation, ω_detection) → couplings, energy transfer pathways.
  Cross-domain: NMR COSY → optical 2D, quantum process tomography.
trigger:
  - designing pump-probe or multidimensional spectroscopy experiments
  - extracting dephasing times from photon echo measurements
  - interpreting 2D spectral maps for molecular dynamics
reasoning_role: ultrafast_spectroscopy
parent: reasoning.uo.pulse_characterization_frog
retrieval_cost: 1
sign_convention: >
  Pump-probe: positive Δt = probe arrives after pump. Photon echo:
  pulse ordering 1→2→3, echo at t = 2τ₂₃ + τ₁₂. Inhomogeneous broadening
  → photon echo; homogeneous → free induction decay (FID). T₂: dephasing
  time. T₁: population relaxation. T₂* = FID decay (includes inhomogeneous).
references:
  - electrodynamics: reasoning.em.optical_coherence (coherence T₂)
  - ultrafast-optics: reasoning.uo.pulse_characterization_frog (FROG parent — GP algorithm for 2D)
---

# reasoning.uo.ultrafast_spectroscopy — Pump-Probe → Photon Echo → 2D Maps

## Core Picture

Ultrafast spectroscopy uses femtosecond pulses to excite a system and a
delayed probe pulse to measure the time-dependent response. At the simplest
level, pump-probe measures excited-state population dynamics. Photon echo
spectroscopy separates homogeneous from inhomogeneous broadening, measuring
the true dephasing time T₂. Two-dimensional (2D) spectroscopy generalizes
this to a full correlation map between excitation and detection frequencies,
revealing couplings, energy transfer pathways, and quantum coherences — the
optical analog of multidimensional NMR (Weiner §12-13; Diels-Rudolph §8;
Mukamel 1995).

## Derivation Sketch — Response Function Formalism

Following Mukamel §5-6, the optical polarization is expanded in orders of
the external field:
```
P = P⁽¹⁾ + P⁽²⁾ + P⁽³⁾ + ...
P⁽ⁿ⁾(t) = ∫₀^∞ dt_n ... ∫₀^∞ dt₁ R⁽ⁿ⁾(t_n,...,t₁) E(t−t_n)...E(t−t_n−...−t₁)
```
where R⁽ⁿ⁾ is the n-th order response function. Linear spectroscopy
(absorption, refraction) is governed by R⁽¹⁾. All ultrafast nonlinear
spectroscopies — pump-probe, photon echo, transient grating, 2D — are
governed by the **third-order response function R⁽³⁾(t₃,t₂,t₁)**.

### 1. Four Liouville-space pathways (R1–R4)

The third-order response decomposes into four distinct density-matrix
pathways (double-sided Feynman diagrams, Mukamel §6):

| Pathway | t₁ evolution | t₂ evolution | t₃ evolution | Physical process |
|---------|-------------|-------------|-------------|-----------------|
| R₁ (NR) | |g⟩⟨e| (coherence) | |e⟩⟨e| (population) | |e⟩⟨g| (coherence) | Excited-state emission (non-rephasing) |
| R₂ (R) | |e⟩⟨g| (coherence) | |e⟩⟨e| (population) | |e⟩⟨g| (coherence) | Excited-state emission (rephasing) |
| R₃ (R) | |e⟩⟨g| (coherence) | |g⟩⟨g| (population) | |e⟩⟨g| (coherence) | Ground-state bleach (rephasing) |
| R₄ (NR) | |g⟩⟨e| (coherence) | |g⟩⟨g| (population) | |e⟩⟨g| (coherence) | Ground-state bleach (non-rephasing) |

**Rephasing** (R₂,R₃): t₁ evolution with phase e^{−iωt₁}, t₃ with e^{+iωt₃}
→ inhomogeneous dephasing reversed → photon echo at t₃ = t₁.
Phase-matching: **k_I = −k₁ + k₂ + k₃**.

**Non-rephasing** (R₁,R₄): same phase sign in t₁ and t₃ → no echo.
Phase-matching: **k_II = +k₁ − k₂ + k₃**.

All four pathways are required for the absorptive 2D spectrum (R₁+R₂+R₃+R₄).

### 2. Photon echo as four-wave mixing

Photon echo is a **third-order four-wave mixing process** (Mukamel §10):
```
Pulse 1 (k₁, t=0) → coherence |g⟩⟨e| (phase e^{−iω_{eg}t₁})
Pulse 2 (k₂, t=t₁) → population |e⟩⟨e| (phase frozen during t₂)
Pulse 3 (k₃, t=t₁+t₂) → coherence |e⟩⟨g| (phase e^{+iω_{eg}t₃})
Signal at k_s = −k₁ + k₂ + k₃ → echo at t₃ = t₁
```
Echo amplitude: |E_echo| ∝ exp(−2t₁/T₂) · exp(−t₂/T₁).
Inhomogeneous distribution contributes factor χ(t₃−t₁) → integrated out
at t₃=t₁ (the echo peak). Homogeneous dephasing T₂ survives.

**Two-pulse echo**: t₂ = 0 (pulses 2 and 3 degenerate).
**Three-pulse (stimulated) echo**: finite t₂ probes population relaxation
and spectral diffusion.

### 3. Pump-probe from response function

Pump-probe signal = heterodyne-detected third-order response:
```
ΔT/T(τ) ∝ Im{P⁽³⁾(t; pump, pump, probe)} ∝ Im{R⁽³⁾ convoluted with fields}
```
Three contributions (all from R⁽³⁾ pathways):
- **Ground-state bleach (GSB)** — R₃+R₄: pump removes g-population
- **Stimulated emission (SE)** — R₁+R₂: pump creates e-population
- **Excited-state absorption (ESA)** — additional e→f transition not in R1-R4
Net: ΔT/T = GSB + SE − ESA.

### 1. Pump-probe spectroscopy

A pump pulse excites the sample; a time-delayed probe pulse measures the
change in transmission ΔT(t)/T₀:
```
ΔT(τ)/T₀ ∝ exp(−τ/T₁)    [population decay, T₁ = energy relaxation time]
```
For electronic transitions in molecules: T₁ ∼ ps-ns. For vibrational: T₁ ∼ ps.

**Transient absorption** spectra: white-light probe (supercontinuum) after
pump → ΔA(λ,τ) = −log₁₀[T_on(λ,τ)/T_off(λ)].

### 2. Photon echo — measuring T₂ (Diels-Rudolph §8)

**Two-pulse photon echo**:
```
Pulse 1: creates coherent superposition (π/2 pulse)
Pulse 2: time-reverses the inhomogeneous dephasing (π pulse)
Echo: appears at t = 2τ (τ = pulse separation)
Echo amplitude: ∝ exp(−2τ/T₂)
```
The echo decays with the HOMOGENEOUS dephasing time T₂, eliminating
the inhomogeneous broadening that masks T₂ in FID (free induction decay
∝ exp(−t/T₂*) with T₂* < T₂).

**Three-pulse photon echo** (stimulated echo):
```
Pulse 1 (τ₁₂)→ Pulse 2 (T)→ Pulse 3 → echo at t = τ₁₂ after pulse 3
Echo ∝ exp(−2τ₁₂/T₂) · exp(−T/T₁)
```
Separates T₂ and T₁ contributions. Allows measurement of spectral diffusion:
as T increases, inhomogeneous environments exchange → T₂ appears longer.

### 3. 2D electronic/vibrational spectroscopy

Three pulses with controlled delays τ (coherence time), T (waiting/population
time), and t (detection time):

```
k₁ (t=0) → k₂ (t=τ) → k₃ (t=τ+T) → signal (t=τ+T+t_detect)
```

Fourier transform τ → ω_τ (excitation axis), t → ω_t (detection axis):
```
S(ω_τ, T, ω_t) = 2D correlation spectrum at waiting time T
```

**Two signal directions** (phase-matching):
- **Rephasing (k_I = −k₁ + k₂ + k₃)**: inhomogeneous broadening refocused.
  Diagonal peaks (ω_τ = ω_t) = same transition excited and detected.
- **Non-rephasing (k_II = +k₁ − k₂ + k₃)**: broadening not refocused.
  Cross peaks (ω_τ ≠ ω_t) = excitation at ω_a, detection at ω_b → coupling.

**Waiting time T evolution**:
- At T = 0: diagonal peaks broadened along diagonal (inhomogeneous).
  Cross peaks = electronic/vibrational coupling.
- As T increases: cross peaks grow from energy transfer, diagonal peaks
  narrow from spectral diffusion, new peaks from chemical reaction products.

### 4. Retrieval: phasing of 2D spectra

The 2D signal is heterodyne-detected: E_sig(t) beats with a local oscillator
E_LO. The complex signal Ẽ_sig(ω_t) is obtained. Phasing uses the projection-
slice theorem:
```
Pump-probe signal = projection of 2D spectrum onto ω_t axis
```
Independent pump-probe measurement → global phase correction.

### 5. Key observables in 2D spectra

| Feature | Physical meaning |
|---------|-----------------|
| Diagonal peak | Same state excited and detected |
| Cross peak (below diagonal) | Excitation at ω_a → population transfer → detection at ω_b (downhill ET) |
| Cross peak (above diagonal) | Uphill energy transfer (thermal activation) |
| Elongation along diagonal | Inhomogeneous broadening |
| Nodal line in peak shape | Excited-state absorption (ESA) overlapping with bleach/stimulated emission |
| Quantum beat (oscillation vs T) | Electronic/vibrational coherence between states |

## Algorithm — Given System → Spectroscopy Design

```
1. IDENTIFY timescales: T₁ (population, ps-ns), T₂ (dephasing, fs-ps),
   energy transfer rates, spectral diffusion times.

2. CHOOSE technique:
   - Population kinetics → pump-probe with white-light supercontinuum.
   - Dephasing (T₂) → photon echo.
   - Couplings / energy transfer → 2D spectroscopy.
   - Vibrational dynamics → IR pump-probe or 2D-IR.

3. PULSE REQUIREMENTS:
   τ_pulse < T₂ to coherently excite the transition.
   Bandwidth > spectral width of transition.
   Energy: avoid multiphoton excitation and sample damage.

4. DETECTION: Heterodyne for 2D (phase information). Direct for pump-probe.
   Spectrometer: CCD or array detector for visible, MCT for IR.

5. ANALYSIS:
   - Exponential fits → T₁, T₂, energy transfer rates.
   - 2D peak shapes → inhomogeneous broadening, FFCF (frequency fluctuation
     correlation function).
   - Center-line slope → FFCF without full 2D lineshape fitting.
```

## Cross-Domain Connection

2D optical spectroscopy is the direct analog of 2D NMR (COSY, NOESY):
```
NMR:     RF pulses → nuclear spin coherence → chemical shift correlation
Optical: fs pulses → electronic/vibrational coherence → transition frequency correlation
```
The pulse sequence and phase-cycling are identical; only the frequency
scale (MHz → THz) and interaction (magnetic dipole → electric dipole)
change. This realization (Ernst, Mukamel) is one of the deepest cross-domain
connections in spectroscopy.

## Cross-References

- Weiner §12-13; Diels-Rudolph §8; Mukamel 1995; Ernst (NMR→optical)
- electrodynamics: reasoning.em.optical_coherence (parent — T₂, optical Bloch equations)
- ultrafast-optics: reasoning.uo.pulse_characterization_frog (FROG for 2D phase retrieval)
- ultrafast-optics: knowledge.uo.ultrafast_spectroscopy_methods (implementation details)
