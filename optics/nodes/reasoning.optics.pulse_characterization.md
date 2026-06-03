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

### SPIDER (Spectral Phase Interferometry)

```
1. Create two time-delayed replicas of E(t).
2. Sum-frequency mix each with a chirped reference → two frequency-sheared replicas.
3. Spectral interferogram: I(ω)=|E(ω)+E(ω+Ω)e^{iωτ}|²
   → fringes encode phase difference φ(ω+Ω)−φ(ω).
4. Direct algebraic phase reconstruction (no iteration!).
   τ_p < 100 fs: SPIDER is faster than FROG. τ_p < 10 fs: FROG more accurate.
```

## Edge Cases

- **Few-cycle pulses** (< 5 fs): SHG crystal phase-matching bandwidth insufficient.
  Use surface SHG (ultrathin crystal) or attosecond streaking.
- **Spatio-temporal coupling**: pulse front tilt, spatial chirp → 3D measurement needed.
- **CEP (carrier-envelope phase)**: critical for few-cycle pulses. f-2f interferometry
  for CEP stabilization. Attosecond streaking for CEP measurement.

## Cross-References

- Trebino §4-12
- electrodynamics: reasoning.em.optical_coherence (Wiener-Khinchin: spectrum from correlation)
