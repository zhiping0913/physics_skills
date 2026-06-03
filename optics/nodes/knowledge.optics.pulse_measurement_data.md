---
skill_id: knowledge.optics.pulse_measurement_data
type: knowledge
summary_50t: >
  AC: G₂(τ)=∫I(t)I(t−τ)dt, width×k (k=√2 Gauss, 1.54 sech²). FROG: 2D
  trace→iterative retrieval→E(t). SPIDER: Ω-sheared spectral interferometry→
  φ(ω) directly. GRENOUILLE: simplified single-shot SHG-FROG. d-scan: dispersion
  scan+phase retrieval. Few-cycle: attosecond streaking, stereo-ATI.
trigger: selecting pulse measurement technique, interpreting FROG traces
reasoning_role: pulse_meas_data
parent: reasoning.optics.pulse_characterization
retrieval_cost: 1
---

# knowledge.optics.pulse_measurement_data

**Autocorrelation**: SHG crystal (BBO, KDP). G₂(τ)=∫I(t)I(t−τ)dt.
Width ratio: Δτ_AC/Δτ_pulse = 1.41 (Gaussian), 1.54 (sech²), 1.66 (asymmetric).
Gives ONLY width, not shape or phase. Always symmetric even if I(t) is not.

**FROG variants**:
- SHG-FROG: E_sig=E(t)E(t−τ). Simplest, symmetric → time-direction ambiguity.
  Sensitive (∝I²), good for Ti:Sapph (∼nJ pulses).
- PG-FROG (polarization gating): E_sig=E(t)|E(t−τ)|². Requires >1μJ. Best for UV.
- THG-FROG: E_sig=E²(t)E(t−τ). More complex trace, no ambiguity.
- XFROG: gate with KNOWN reference pulse. Measures weak/arbitrary pulses.
- GRENOUILLE: replaces spectrometer+delay with Fresnel biprism+thick crystal.
  Single-shot, alignment-free SHG-FROG.

**FROG retrieval error**: G = √(Σ|I_meas−I_ret|²/N²). G<0.01 is excellent.
The trace is N×N overdetermined → robust convergence. Typical: 50-200 iterations.

**SPIDER**: spectral shear Ω∼1-5THz (from chirped pulse). Delay τ∼ps.
φ(ω) from Fourier transform of I(ω)=|E(ω)+E(ω+Ω)e^{iωτ}|² → algebraic, no iteration.
Accuracy ∼0.01 rad. Best for τ_p<50fs.

**d-scan**: measure spectrum vs inserted dispersion (D-scan trace).
Iterative retrieval similar to FROG. Self-calibrating.

**Few-cycle/attosecond**: FROG-CRAB (attosecond streaking). Stereo-ATI.
CEP measurement: f-2f interferometry (f_CEO), stereo-ATI (few-cycle).

- Trebino §5-12, §16-18
