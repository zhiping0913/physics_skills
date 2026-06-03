---
skill_id: reasoning.optics.pulse_characterization
type: reasoning
summary_50t: >
  A pulse cannot measure itself → need nonlinear gate. Autocorrelation
  gives width, not shape. FROG: spectrally-resolved autocorrelation →
  2D trace → iterative phase retrieval → E(t) amplitude+phase.
  SPIDER: spectral interferometry between two frequency-sheared replicas.
trigger:
  - measuring femtosecond/attosecond pulse shape and phase
  - characterizing dispersion, chirp of ultrashort pulses
reasoning_role: pulse_measurement
parent: reasoning.em.optical_coherence
retrieval_cost: 1
sign_convention: >
  E(t) = √I(t) exp(iφ(t)) — temporal phase φ(t) via FROG/SPIDER.
  Positive chirp: dω/dt > 0 (instantaneous frequency increases with time,
  red leads blue). GDD = d²φ/dω²; positive GDD → positive chirp.
  FROG delay τ: positive = gate arrives after probe.
references:
  - electrodynamics: reasoning.em.optical_coherence (time-frequency uncertainty)
---

# reasoning.optics.pulse_characterization — Nonlinear Gate → E(t)

## Core Picture

An ultrashort pulse is shorter than any electronic detector's response time.
To measure it, the pulse must gate ITSELF using a nonlinear optical process
(second harmonic generation, polarization gating, etc.). This is the
fundamental principle: **a pulse cannot be measured without a shorter
reference — so it must provide its own** (Trebino §4).

## Derivation Sketch

Starting from `electrodynamics: reasoning.em.optical_coherence` (the
Wiener-Khinchin theorem: the power spectrum is the Fourier transform of the
autocorrelation function — but this gives ONLY the spectrum, not the
phase; a pulse is defined by BOTH amplitude and phase):

1. **Why autocorrelation is insufficient** (consuming parent edge):
   From optical_coherence, the intensity autocorrelation:
   ```
   G₂(τ) = ∫ I(t) I(t−τ) dt
   ```
   yields the Fourier transform of the POWER SPECTRUM (by Wiener-Khinchin:
   |G₂(τ)| ↔ |E(ω)|²). This gives the pulse WIDTH but NOT the shape: any
   symmetric I(t) produces a symmetric G₂(τ). The spectral PHASE φ(ω) is
   completely lost. The parent node establishes the time-frequency duality;
   this node extends it to the nonlinear domain required for RECOVERING
   the lost phase information.

2. **The gate-pulse trick** (key non-obvious step — Trebino §4-5):
   To recover phase, we need a TIME-FREQUENCY spectrogram:
   ```
   S(ω,τ) = |∫ E_sig(t,τ) e^{iωt} dt|²
   ```
   where E_sig(t,τ) = nonlinear interaction of E(t) with a gate G(t−τ).
   This is exactly the SHORT-TIME FOURIER TRANSFORM of the pulse — if the
   gate were a delta function, S(ω,τ) would be a perfect spectrogram.
   But NO electronic gate is fast enough for fs pulses. The resolution:
   use the pulse as its own gate via nonlinear mixing → FROG.

3. **Phase retrieval from 2D trace** (iterative algorithm):
   FROG produces an N×N 2D trace (overdetermined: N² data points for 2N
   unknowns — N amplitude + N phase). The generalized projections algorithm
   alternates between:
   - Time-domain constraint: E_sig(t,τ) = E(t) G(t−τ) (physical form)
   - Frequency-domain constraint: |FT{E_sig}| = √I_FROG(ω,τ) (data)
   Convergence is robust because the problem is massively overdetermined.
   This is the same mathematical structure as 2D phase retrieval in
   coherent diffraction imaging (the same Gerchberg-Saxton / Fienup
   algorithm family used in X-ray ptychography).

## Algorithm: From Data to E(t)

### Intensity Autocorrelation

```
G₂(τ) = ∫ I(t) I(t−τ) dt   (background-free, SHG)
Width: Δτ_AC = k·Δτ_pulse (k=√2 for Gaussian, 1.54 for sech²).
Gives pulse WIDTH, not shape. Any symmetric I(t) gives symmetric G₂.
Contrast ratio: 8:1 (interferometric), 3:1 (background-free).
```

### FROG (Frequency-Resolved Optical Gating)

```
1. Gate pulse with replica: E_sig(t,τ) = E(t) G(t−τ) [PG], E(t)|E(t−τ)|² [SHG].
2. Spectrally resolve: I_FROG(ω,τ) = |∫ E_sig(t,τ) e^{iωt} dt|².
3. 2D iterative phase retrieval: project between time and frequency domains,
   enforcing data constraint (measured I_FROG) and physical constraint (E_sig form).
4. Output: E(t) = √I(t) e^{iφ(t)} — full amplitude AND phase.

FROG trace is N×N (overdetermined) → robust, self-consistency check.
PG-FROG: best for UV/visible. SHG-FROG: simplest, but time-direction ambiguous.
GRENOUILLE: simplified SHG-FROG (single shot, no spectrometer needed).
```

**Single-shot FROG** (Trebino §10-12): Replace the scanning delay line with
a spatial encoding of delay: cross the two beams at an angle → delay varies
linearly across the beam profile. A single camera exposure captures the
entire FROG trace. GRENOUILLE (GRating-Eliminated No-nonsense Observation
of Ultrafast Incident Laser Light E-fields) does this with a thick SHG
crystal at the crossing point — the phase-matching bandwidth limits the
wavelength range, and the beam crossing encodes the delay. Single-shot
operation is essential for:
- Low-repetition-rate systems (kHz) where scanning takes hours
- Shot-to-shot fluctuation studies (pulse instability diagnosis)
- High-energy systems where every shot matters

### SPIDER (Spectral Phase Interferometry)

```
1. Create two time-delayed replicas of E(t).
2. Sum-frequency mix each with a chirped reference → two frequency-sheared replicas.
3. Spectral interferogram: I(ω)=|E(ω)+E(ω+Ω)e^{iωτ}|²
   → fringes encode phase difference φ(ω+Ω)−φ(ω).
4. Direct algebraic phase reconstruction (no iteration!).
   τ_p < 100 fs: SPIDER is faster than FROG. τ_p < 10 fs: FROG more accurate.
```

### d-scan (Dispersion Scan — Miranda 2012)

A complementary method for few-cycle pulse characterization:
```
1. Insert variable-thickness dispersive material (wedge pair) in the beam.
2. Measure SHG spectrum as a function of inserted GDD.
3. The 2D trace (SHG spectrum vs. GDD) is compared to a simulated trace
   derived from the NLSE propagation of a trial pulse through the same GDD.
4. Iteratively optimize the trial pulse's spectral phase to match measured trace.
```
Advantage over FROG/SPIDER: NO beam splitting, NO delay scanning — the
dispersion is varied along the SAME beam path. Inherently aligned, single-beam
geometry. Excellent for few-cycle pulses (< 5 fs) where beam splitting
introduces alignment errors and additional dispersion mismatch. The d-scan
trace IS the pulse compressor diagnostic — you can compress while measuring
(on-the-fly optimization). Reference: Miranda et al., Opt. Express 20, 688 (2012).

## Attosecond Pulse Characterization

**Attosecond streaking** (Krausz & Ivanov, RMP 81, 163, 2009):
A synchronized few-cycle NIR laser field (the "streaking field") ionizes
atoms in the presence of the attosecond XUV pulse. The photoelectron
momentum is shifted by the vector potential A(t) of the streaking field
at the instant of ionization. Scanning the delay between XUV and NIR →
p(t) = p₀ − e A(t_delay) → the electron spectrogram maps the attosecond
pulse envelope AND the streaking field. From this, both the attosecond
pulse duration and the CEP of the streaking field are reconstructed.

**RABBIT** (Reconstruction of Attosecond Beating By Interference of
Two-photon transitions — Paul 2001):
An attosecond pulse train (APT, from high-harmonic generation) photoionizes
atoms in the presence of a weak NIR dressing field. Each harmonic q
produces a main photoelectron line; the dressing field adds sidebands at
energies q+1 and q−1. The sideband intensity oscillates with the XUV-NIR
delay at 2ω_NIR, and the phase of this oscillation encodes the RELATIVE
phase between adjacent harmonics → reconstructs the attosecond chirp.
RABBIT measures the GROUP DELAY of the attosecond pulse train (emission
time vs. harmonic order) but NOT the carrier-envelope phase of individual
attosecond pulses (which requires streaking with few-cycle NIR).

## Edge Cases

- **Few-cycle pulses (< 5 fs)**: SHG crystal phase-matching bandwidth insufficient.
  Use surface SHG (10-20 μm BBO, or even 1-2 μm for sub-3-fs), d-scan
  (no SHG crystal bandwidth required if using two-photon absorption in a
  semiconductor detector), or attosecond streaking (XUV regime, no crystal
  needed — free-electron detection).
- **Spatio-temporal coupling**: pulse front tilt, spatial chirp → 3D measurement
  needed. Standard 1D FROG/SPIDER assumes no spatio-temporal coupling.
  For pulses with spatial chirp, use SEA-FROG (spatially encoded arrangement
  FROG) or STRIPED-FISH (scanning SEA TADPOLE) — 3D measurement (x,y,t).
  Reference: Gabolde & Trebino, Opt. Express 14, 9623 (2006).
- **CEP (carrier-envelope phase)**: critical for few-cycle pulses. f-2f
  interferometry for CEP stabilization. For ATTOSECOND CEP measurement:
  stereo-ATI (above-threshold ionization) — left-right electron asymmetry
  encodes CEP in few-cycle pulses. Attosecond streaking directly reveals
  CEP via the offset of the streaking spectrogram.
- **Low-repetition-rate systems (< 10 kHz)**: Scanning FROG is too slow.
  Use GRENOUILLE (single-shot SHG-FROG) or single-shot SPIDER (SEA-SPIDER:
  spatially encoded arrangement SPIDER). Pulse-to-pulse stability measurement
  requires single-shot capability.
- **High-energy pulses**: Nonlinear detector damage threshold limits
  measurement. Use attenuated pickoff + surface SHG (thin crystal, no
  tight focusing) or transient-grating FROG (TG-FROG, uses third-order
  nonlinearity in bulk glass — higher damage threshold, self-referenced).

## Cross-References

- Trebino §4-12
- electrodynamics: reasoning.em.optical_coherence (Wiener-Khinchin: spectrum from
  correlation; parent edge: Derivation Sketch step 1 shows autocorrelation
  alone is insufficient — the phase loss inherent in the Wiener-Khinchin
  theorem motivates the nonlinear gate method)
- optics: reasoning.optics.dispersion_management_gdd (GDD measurement: FROG/
  SPIDER measure spectral phase φ(ω) → φ₂ = d²φ/dω² = GDD. Bidirectional:
  dispersion_management provides the GDD that must be measured; pulse_characterization
  provides the measurement tool)
