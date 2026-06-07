---
skill_id: reasoning.uo.carrier_envelope_phase
type: reasoning
summary_50t: >
  CEP φ_CEO: offset between carrier and envelope peak. v_g ≠ v_φ →
  Δφ_CEO = 2πL(1/v_g − 1/v_φ) per pass. Comb equation: f_n = n f_rep + f_CEO
  where f_CEO = f_rep·Δφ_CEO/(2π). f-2f interferometer: octave spectrum →
  SHG of low-f end beats with high-f end → f_CEO measurement. Feed-forward
  (AOM) or feed-back (pump power) stabilization to <100 mrad.
trigger:
  - designing CEP stabilization for few-cycle pulse sources
  - understanding comb offset frequency from CEP slip
  - interpreting f-2f interferometer signals
reasoning_role: cep_control
parent: reasoning.uo.mode_locking_passive
retrieval_cost: 1
sign_convention: >
  CEP = φ_CEO = φ_carrier − φ_envelope at pulse peak. Δφ_CEO per round-trip
  = 2πL(1/v_g − 1/v_φ) mod 2π. f_CEO = (Δφ_CEO/2π) · f_rep, 0 ≤ f_CEO < f_rep.
  Positive Δφ_CEO → carrier advances relative to envelope each round-trip.
references:
  - ultrafast-optics: reasoning.uo.mode_locking_passive (oscillator)
  - ultrafast-optics: reasoning.uo.frequency_comb (comb equation)
  - ultrafast-optics: reasoning.uo.attosecond_pulse_generation (CEP for IAP)
---

# reasoning.uo.carrier_envelope_phase — v_g ≠ v_φ → Δφ_CEO → f_CEO

## Core Picture

In a mode-locked laser, the carrier wave and the pulse envelope travel at
different velocities (v_φ ≠ v_g) inside the cavity. This causes the carrier
to slip relative to the envelope by Δφ_CEO each round-trip. For few-cycle
pulses, this CEP determines the peak electric field and is critical for
attosecond science. The CEP slip manifests in the frequency domain as the
carrier-envelope offset frequency f_CEO, the "0th" tooth of the frequency
comb (Ye-Cundiff §2-5; Weiner §2.7; Hänsch 1978).

## Derivation Sketch

### 1. CEP slip per round-trip

After one round-trip through a cavity of length L:
```
Carrier advances by:  φ_carrier = ω_c L/v_φ = 2πL/λ_c
Envelope advances by: φ_envelope = ω_c L/v_g
```
The CEP shift per round-trip:
```
Δφ_CEO = φ_carrier − φ_envelope = ω_c L (1/v_φ − 1/v_g)    (mod 2π)
```

For a dispersive cavity, both v_φ and v_g are average values over the
intracavity elements. In a typical Ti:sapphire oscillator, Δφ_CEO is
random (not constant) without stabilization — the comb is "free-running."

### 2. From Δφ_CEO to f_CEO — the comb equation

Consider the pulse train in time: E(t) = Σ_n a(t−nT_R) e^{i(ω_c t − nΔφ_CEO)}.
Fourier transform yields a comb of frequencies:
```
f_n = n f_rep + f_CEO
where f_CEO = (Δφ_CEO/2π) · f_rep
```
f_rep = 1/T_R is the repetition rate (∼80-100 MHz for Ti:sapphire).
f_CEO is the carrier-envelope offset frequency (typically 0 to f_rep).

### 3. f-2f self-referencing (Ye-Cundiff §3, Telle 1999)

To measure f_CEO, the comb must span a full OCTAVE (ν_max > 2ν_min).
For an octave-spanning comb (e.g., 500-1000 nm):

**f-2f interferometer**:
```
Step 1: Take comb line n at frequency f_n = n f_rep + f_CEO   (in IR, e.g., 1000 nm)
Step 2: Frequency-double it: 2f_n = 2n f_rep + 2f_CEO       (now at ∼500 nm)
Step 3: Beat with comb line 2n at 2f_n − f_2n:
        f_beat = (2n f_rep + 2f_CEO) − (2n f_rep + f_CEO) = f_CEO
```
The beat note directly gives f_CEO! This is the enabling technology for
optical frequency metrology — Nobel Prize in Physics 2005 (Hänsch & Hall).

### 4. CEP stabilization methods

**Feed-back (slow, <100 kHz bandwidth)**:
- Modulate pump laser power → changes intracavity peak power → changes
  nonlinear phase → shifts Δφ_CEO.
- Bandwidth limited by gain dynamics (∼100 kHz).
- Residual CEP jitter: ∼100-300 mrad (rms, integrated).

**Feed-forward (fast, >1 MHz bandwidth)**:
- Measure Δφ_CEO via f-2f on a single-shot basis.
- Apply compensating phase shift via an AOM (acousto-optic modulator)
  placed AFTER the oscillator.
- Bandwidth: limited by AOM response (∼1-10 MHz).
- Residual CEP jitter: <100 mrad.

**Slow + fast combination**: Feed-back for long-term drift (<100 Hz),
feed-forward for fast fluctuations (100 Hz–1 MHz) → <70 mrad jitter.

### 5. CEP effects on few-cycle pulses

For a pulse with duration τ_p and CEP φ_CEO:
```
E(t) = E₀ sech(t/τ_p) cos(ω_c t + φ_CEO)
```
The peak field E_peak depends on φ_CEO — for τ_p < 2 optical cycles,
E_peak varies by up to 100% as φ_CEO drifts. CEP-stabilized pulses are
essential for:
- Isolated attosecond pulse generation (IAP — needs cos-like E-field)
- Attosecond streaking (CEP controls streaking spectrogram)
- Carrier-envelope phase-dependent strong-field physics (above-threshold
  ionization, high-harmonic generation)

## Algorithm — Given Comb → f_CEO Measurement + Stabilization

```
1. GENERATE octave-spanning spectrum:
   - Ti:sapphire oscillator + photonic crystal fiber (PCF) for supercontinuum
   - Or: directly octave-spanning oscillator (DCM mirrors)
   - Or: Er:fiber comb with highly nonlinear fiber (HNLF)

2. f-2f SETUP:
   - Dichroic split: long-λ (>1000 nm) and short-λ (<500 nm).
   - SHG of long-λ end in a PPLN or BBO crystal.
   - Overlap SHG with short-λ end on a photodiode → measure f_beat.

3. STABILIZE f_CEO:
   - Lock f_CEO to a stable reference (RF synthesizer or atomic clock).
   - Error signal → PID controller → pump power (feed-back) or AOM (feed-forward).

4. STABILIZE f_rep (separately):
   - Lock f_rep to RF reference by cavity length control (PZT on end mirror).

5. VERIFY: f_CEO linewidth <1 Hz (locked), integrated CEP jitter <100 mrad.
   Measure out-of-loop f-2f (independent interferometer) for true stability.
```

## Edge Cases

- **Insufficient octave for f-2f**: Use 2f-3f interferometer (needs 2/3 octave)
  or common-path f-2f in PCF.
- **CEP slip in amplifier chain**: Chirped pulse amplifier stretches the pulse →
  CEP in the amplifier is "frozen" for ps duration. But stretcher/compressor
  misalignment adds CEP noise.
- **CEP drift in hollow-core fiber**: Ionization in gas-filled fiber produces
  plasma-dependent dispersion that drifts CEP. Requires active slow-loop
  stabilization after HCF.

## Cross-References

- Ye-Cundiff §2-5; Telle 1999; Jones 2000
- ultrafast-optics: reasoning.uo.frequency_comb (f_n = n f_rep + f_CEO application)
- ultrafast-optics: reasoning.uo.mode_locking_passive (oscillator source)
- ultrafast-optics: reasoning.uo.attosecond_pulse_generation (CEP for IAP selection)
