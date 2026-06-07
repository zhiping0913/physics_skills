---
skill_id: reasoning.uo.pulse_characterization_spider_dscan
type: reasoning
summary_50t: >
  SPIDER: spectral interferometry between two replicas frequency-sheared by
  Ω via sum-frequency with chirped ancilla. Phase extracted from fringe
  spacing: φ(ω+Ω)−φ(ω) ∝ fringe deviation. d-scan: dispersion scan — measure
  SHG spectrum vs added GDD; MIIPS retrieval from 2D trace. SPIDER: direct,
  analytic, single-shot. d-scan: easy alignment, self-calibrating. Both
  complement FROG for different measurement regimes.
trigger:
  - choosing between FROG, SPIDER, and d-scan for a given pulse measurement
  - implementing SPIDER or d-scan phase retrieval
  - interpreting SPIDER interferograms or d-scan traces
reasoning_role: spider_dscan_measurement
parent: reasoning.uo.pulse_characterization_frog
retrieval_cost: 1
sign_convention: >
  SPIDER shear Ω > 0: ω-shifted replica to higher frequency.
  SPIDER delay τ fixed between unsheared replicas. d-scan: added
  GDD > 0 (normal dispersion) → pulse broadens. MIIPS: reference
  phase φ_MIIPS(ω) scanned via pulse shaper.
references:
  - ultrafast-optics: reasoning.uo.pulse_characterization_frog (sibling)
  - ultrafast-optics: reasoning.uo.pulse_propagation_linear (ψ₂, chirp)
---

# reasoning.uo.pulse_characterization_spider_dscan — Spectral Shear + Dispersion Scan → φ(ω)

## Core Picture

SPIDER (Spectral Phase Interferometry for Direct Electric-field Reconstruction,
Iaconis & Walmsley 1998) and d-scan (Dispersion Scan, Miranda 2012) provide
alternatives to FROG for ultrashort pulse characterization. SPIDER extracts
the spectral phase **directly and analytically** from a single interferogram
— no iterative retrieval needed. d-scan simultaneously compresses and
characterizes the pulse — self-calibrating because the same dispersion is
used for compression and measurement (Diels-Rudolph §10, Dantus §4-5).

## Derivation Sketch

### 1. SPIDER — spectral shear interferometry

**Experimental layout**:
```
Input pulse → BS → [arm1: chirped ancilla (stretched to ps)]
                  [arm2: split, delay τ → two replicas]
                  ↓
  SFG in χ⁽²⁾ crystal: replica1 + ancilla(t) → ω + ω_anc
                         replica2 + ancilla(t+τ) → ω + Ω + ω_anc
  where Ω = frequency shear from ancilla chirp
                  ↓
  Spectrometer: interferogram I(ω) = |E(ω)+E(ω+Ω)e^{iωτ}|²
```

**Ancilla chirp → frequency shear** (key insight):
A strongly chirped ancilla pulse has instantaneous frequency
ω_anc(t) = ω₀ + (t/ψ₂_anc). Two replicas separated by τ undergo SFG
with ancilla at different instants → their sum-frequency outputs are
shifted in frequency by:
```
Ω = τ / ψ₂_anc          [shear; typically 1-5% of bandwidth]
```

**Phase retrieval** (analytic, no iteration):
```
I(ω) = |E(ω)|² + |E(ω+Ω)|² + 2|E(ω)||E(ω+Ω)| cos[φ(ω+Ω)−φ(ω) + ωτ]

From fringe positions: extract Δφ(ω) = φ(ω+Ω)−φ(ω)
Integrate (concatenate): φ(ω) = Σ_ω Δφ(ω)
Calibrate: remove linear term (τ). Remove quadratic from shear calibration.
```

**SPIDER advantages**:
- Direct (non-iterative) → fast, unambiguous
- Single-shot capable (no moving parts)
- Works for complex pulses (satellite pulses, multi-pulsing visible in interferogram)

**SPIDER limitations**:
- Ancilla chirp must be well-characterized
- Shear Ω must be small enough to resolve fringes, large enough for sensitivity
- Ancilla must have bandwidth exceeding the test pulse
- Stray spectral amplitude calibration required

### 2. d-scan — dispersion scan

**Experimental layout**:
```
Input pulse → [variable dispersion: wedge pair or pulse shaper]
           → SHG crystal → spectrometer → SHG spectrum vs GDD
```

A known amount of GDD is added to the pulse. For each GDD value, the
SHG spectrum is measured → 2D trace I_SH(ω, GDD_added).

**Physical principle**: When GDD_added compensates the pulse's own chirp,
the pulse becomes transform-limited → SHG spectrum is narrowest (highest
peak). When GDD_added adds to the chirp → pulse broadens → SHG spectrum
narrows and red-shifts.

**d-scan trace features**:
- **Symmetric about zero-chirp point**: For a linearly chirped pulse with
  GDD₀, the SHG trace is symmetric around GDD_added = −GDD₀.
- **TOD signature**: Asymmetric trace distortion.
- **Self-calibration**: The same dispersion elements compress AND
  characterize the pulse.

**MIIPS (Multiphoton Intrapulse Interference Phase Scan)** — retrieval from
d-scan-type data using a pulse shaper to apply reference phase functions.
The phase is retrieved by detecting deviations from the expected SHG
spectrum for each reference phase (Dantus §4).

### 3. Comparison with FROG

| Property | FROG | SPIDER | d-scan |
|----------|------|--------|--------|
| Retrieval | Iterative (GP algorithm) | Direct (analytic) | Iterative or MIIPS |
| Complexity | Moderate (delay scan) | High (ancilla generation) | Low (wedge insertion) |
| Single-shot | GRENOUILLE only | Yes (standard) | No (scan required) |
| Ambiguities | Time direction (SHG) | None | None |
| Complex pulses | Good | Excellent (resolves satellites) | Good |
| Sensitivity | High (SHG-FROG) | Medium | High (SHG) |
| Self-calibrating | No | No | **Yes** |

## Algorithm — Given Measurement → φ(ω)

### SPIDER retrieval
```
1. MEASURE: SPIDER interferogram I_meas(ω). Also measure individual
   spectra |E(ω)|² and |E(ω+Ω)|² by blocking one arm.

2. PREPROCESS:
   - Subtract background
   - Normalize by |E(ω)||E(ω+Ω)|
   - Fourier filter: FFT{I_norm(ω)} → isolate AC peak at ±τ
     → IFFT → pure interference term

3. EXTRACT PHASE DIFFERENCE:
   cos[Δφ(ω)+ωτ] = Re{I_filtered(ω)}
   Δφ_raw(ω) = arccos(…) or Hilbert transform of filtered signal.
   Unwrap phase to remove 2π jumps.

4. CALIBRATE SHEAR Ω:
   Measure τ (arm delay) and ψ₂_anc (ancilla GDD).
   Ω = τ / ψ₂_anc.

5. INTEGRATE:
   φ(0) = 0
   φ(k·Ω) = Σ_{j=0}^{k-1} Δφ(j·Ω)   (concatenate at shear steps)

6. REMOVE LINEAR TERM (group delay) and QUADRATIC term (shear miscalibration).
   Output: φ(ω) in spectral region spanned by shear steps.
```

### d-scan / MIIPS retrieval
```
1. MEASURE: I_SH(ω, GDD_added) for range of added GDD values.

2. IDENTIFY zero-chirp point: GDD_added where SHG signal is maximally
   broadened (or where MIIPS trace shows characteristic features).

3. MIIPS retrieval:
   - Apply reference phases φ_ref(ω; α) = α·cos(γω−δ) via pulse shaper.
   - For each α,δ: SHG spectrum has modulation from intrapulse interference.
   - Compare measured modulation to expected modulation for unchirped pulse.
   - Difference → actual pulse phase φ(ω).

4. OUTPUT: φ(ω) (d-scan) or φ(ω) + optimal compression GDD (MIIPS).
```

## Edge Cases

- **SPIDER: insufficient shear Ω**: Small Ω → phase difference noisy.
  Large Ω → lose fine spectral features. Optimal: Ω ≈ 0.02-0.05 × Δω_FWHM.
- **SPIDER: ancilla bandwidth**: Ancilla must cover the full test pulse
  bandwidth. For octave-spanning pulses → need octave ancilla → supercontinuum.
- **d-scan: thick SHG crystal phase-matching artifacts**: SHG efficiency
  varies with wavelength in thick crystals. Use thin crystal (<20 μm)
  or correct for phase-matching efficiency curve.
- **SPIDER for CEP-stable few-cycle pulses**: Ancilla chirp must be
  known to <1 fs accuracy. Calibrate ancilla phase via independent
  measurement (e.g., SEA-SPIDER variant).

## Cross-References

- Iaconis & Walmsley 1998 (SPIDER), Miranda 2012 (d-scan), Dantus §4-5
- ultrafast-optics: reasoning.uo.pulse_characterization_frog (sibling)
- ultrafast-optics: reasoning.uo.pulse_propagation_linear (GDD→chirp→broadening uses SPIDER-measured φ(ω))
- ultrafast-optics: knowledge.uo.pulse_measurement_techniques (technique selection guide)
