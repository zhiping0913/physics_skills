---
skill_id: reasoning.uo.pulse_characterization_frog
type: reasoning
summary_50t: >
  FROG = spectrally-resolved autocorrelation. SHG-FROG: I_FROG(ω,τ) =
  |∫ E(t)E(t−τ)e^{−iωt}dt|². PG-FROG: gate = |E(t−τ)|² → more intuitive.
  Iterative retrieval: generalized projections (GP) algorithm alternates
  between Fourier constraint (match measured trace) and physical constraint
  (signal = product of fields). FROG error G measures convergence. GRENOUILLE:
  single-shot SHG-FROG using Fresnel biprism + thick SHG crystal.
trigger:
  - retrieving pulse amplitude and phase from FROG measurements
  - choosing FROG variant for a given pulse parameter range
  - debugging FROG retrieval when G stalls
reasoning_role: frog_pulse_measurement
parent: reasoning.uo.pulse_propagation_linear
retrieval_cost: 1
sign_convention: >
  FROG delay τ: positive = gate arrives after probe. PG-FROG: gate = |E(t−τ)|².
  SHG-FROG: symmetric in τ (time direction ambiguity). FROG error G:
  rms difference between measured and retrieved trace, normalized.
  Convergence: G < 0.01 for typical good retrieval.
references:
  - ultrafast-optics: reasoning.uo.pulse_propagation_linear (pulse representation)
---

# reasoning.uo.pulse_characterization_frog — Spectrogram → Iterative Retrieval → E(t)

## Core Picture

Frequency-Resolved Optical Gating (FROG) measures a 2D spectrogram of an
ultrashort pulse by gating it with a delayed replica in a nonlinear medium
and spectrally resolving the generated signal. The resulting FROG trace
I_FROG(ω,τ) is a 2D function that overdetermines the pulse field E(t) —
allowing unique retrieval of both amplitude and phase via iterative
algorithms (Trebino §10-18, Weiner §9, Diels-Rudolph §10).

## Derivation Sketch

### 1. FROG trace generation (Weiner §9.3)

**SHG-FROG** (simplest, most common):
```
E_sig(t,τ) = E(t) · E(t−τ)           [gate = replica of pulse]
I_SHG(ω,τ) = |∫ E_sig(t,τ) e^{−iωt} dt|²
```

**PG-FROG** (polarization gating, more intuitive):
```
E_sig(t,τ) = E(t) · |E(t−τ)|²        [gate = intensity of delayed pulse]
I_PG(ω,τ) = |∫ E_sig(t,τ) e^{−iωt} dt|²
```

**THG-FROG, XFROG**: Third-harmonic, cross-correlation variants for UV/IR.

**Key insight**: The FROG trace is a SPECTROGRAM — the short-time Fourier
transform of E(t) with a gate that is itself derived from the pulse. This
self-referential structure provides the uniqueness guarantee.

### 2. FROG trace symmetries

SHG-FROG is symmetric: I(ω,τ) = I(ω,−τ). This introduces a time-direction
ambiguity — I(t) vs I(−t) produce identical traces. The spectral phase
also has a sign ambiguity. PG-FROG resolves both ambiguities.

**Trace marginals** (Trebino Ch.6):
- ∫I_SHG(ω,τ) **dω** → SHG intensity autocorrelation ∫|E(t)|²|E(t−τ)|²dt (function of τ)
- ∫I_SHG(ω,τ) **dτ** → autoconvolution of |E(ω)|² (function of ω)
Use marginals for consistency checks against independently measured spectrum/autocorrelation.

### 3. Iterative retrieval — Generalized Projections (GP) algorithm

The GP algorithm alternates between two constraint sets (Trebino §17):

```
Initialize: guess E(t) (e.g., random phase + measured spectrum)

REPEAT:
  1. GENERATE signal field:
     E_sig(t,τ) = E(t) · |E(t−τ)|²   [PG-FROG physical constraint]

  2. FOURIER transform: Ẽ_sig(ω,τ) = FFT{E_sig(t,τ)}

  3. APPLY DATA constraint:
     Replace |Ẽ_sig(ω,τ)| with √(I_meas(ω,τ))
     Keep phase of Ẽ_sig(ω,τ) unchanged.

  4. INVERSE FOURIER: E'_sig(t,τ) = IFFT{Ẽ'_sig(ω,τ)}

  5. EXTRACT E(t) from E'_sig(t,τ):
     E(t) = argmin Σ_τ |E'_sig(t,τ) − E(t)·|E(t−τ)|²|²
     [least-squares fit to physical constraint form]

UNTIL FROG error G converges.
```

**FROG error** (rms normalized):
```
G = √[ (1/N²) Σ_{ω,τ} |I_retrieved(ω,τ) − I_meas(ω,τ)|² ]
```
G < 0.01: excellent retrieval. G < 0.005: nearly perfect. G > 0.05:
problematic — algorithm may be stuck.

### 4. GRENOUILLE — single-shot SHG-FROG (O'Shea 1999)

Simplifies SHG-FROG to a single-shot device with no moving parts:
- **Fresnel biprism**: splits and crosses the beam → delay τ mapped to
  transverse position x.
- **Thick SHG crystal**: phase-matching bandwidth limited → acts as the
  spectrometer (frequency-to-angle mapping).

Trade-off: reduced temporal range and spectral resolution compared to
scanning FROG, but alignment-free and single-shot.

## Algorithm — Given FROG Trace → E(t)

```
1. INPUT: I_FROG(ω,τ) [N_ω × N_τ grid], FROG variant (SHG/PG/THG).

2. PREPROCESS:
   - Background subtraction (remove scattering, detector offset).
   - Symmetrize for SHG-FROG: I(ω,τ) = I(ω,−τ) enforced.
   - Filter high-frequency noise (Wiener filter).

3. INITIALIZE:
   - E(t) = √(I_measured(t)) exp(iφ_guess(t)), where φ_guess = 0 or random.
   - Or: use measured spectrum + flat phase as initial guess.

4. GP ITERATION LOOP (typically 100-500 iterations):
   a. Construct E_sig(t,τ) per variant's physical constraint.
   b. FFT to (ω,τ) domain.
   c. Replace magnitude with √(I_meas), keep phase.
   d. IFFT to (t,τ) domain.
   e. Project back to physical constraint form to get new E(t).
   f. Compute G. If G < target → converged.

5. POST-PROCESS:
   - Remove linear spectral phase (group delay).
   - Check time ambiguity for SHG: try both E(t) and E*(−t).
   - Check spectral marginals consistency.

6. OUTPUT: E(t) = √(I(t)) exp(iφ(t)), I(ω) = |Ẽ(ω)|², φ(ω).
   Derived: τ_g(ω) = dφ/dω, ω_inst(t) = −dφ/dt, chirp.
```

## FROG Variant Selection

| Variant | Gate | Sensitivity | Ambiguities | Best for |
|---------|------|------------|-------------|----------|
| SHG-FROG | E(t) | High (χ⁽²⁾) | Time direction + phase sign | Oscillator pulses (>1 nJ) |
| PG-FROG | |E|² | Medium (χ⁽³⁾) | None (intuitive) | Amplified pulses (>1 μJ) |
| THG-FROG | E²(t) | Low (χ⁽³⁾) | None | UV pulses |
| XFROG | Known reference | High | None if reference known | Weak/complex pulses |
| GRENOUILLE | E(t) (single-shot) | Medium | Same as SHG | Alignment-free diagnostics |

## Edge Cases

- **Stagnation**: GP algorithm can get stuck at local minima (G plateaus).
  Remedy: use multiple random initial guesses; switch to "short-cut GP"
  (Trebino §18); add annealing.
- **Noise amplification**: Noise in trace wings propagates into retrieved
  phase at spectral edges where intensity is low. Limit retrieval bandwidth
  to region with SNR > 10.
- **SHG-FROG time ambiguity**: Produce identical traces for E(t) and E*(−t).
  Resolve by measuring spectrum after dispersive element or using PG-FROG.
- **Thick-crystal effects**: In SHG-FROG, phase-matching bandwidth of the
  SHG crystal limits measurable spectral range. Use thin crystal (<100 μm)
  for broadband pulses, with correction for phase-matching efficiency.

## Cross-References

- Trebino §10-18; Weiner §9.3-9.5; Diels-Rudolph §10
- ultrafast-optics: reasoning.uo.pulse_propagation_linear (E(t)↔E(ω) via FT)
- ultrafast-optics: reasoning.uo.pulse_characterization_spider_dscan (alternative methods)
- ultrafast-optics: knowledge.uo.pulse_measurement_techniques (measurement data)
