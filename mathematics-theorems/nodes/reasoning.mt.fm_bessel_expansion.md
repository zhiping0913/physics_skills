---
skill_id: reasoning.mt.fm_bessel_expansion
type: reasoning
summary_50t: >
  sin(ωt + β cos Ωt) = J₀ sin ωt + Σ J_n [sin((ω+nΩ)t) + (−1)ⁿ sin((ω−nΩ)t)]
  + J₁ cos((ω+Ω)t) − J₁ cos((ω−Ω)t) + ... . Jacobi-Anger: e^{iz cos θ} = Σ iⁿ J_n(z) e^{inθ}.
  cos(z cos θ) = J₀ − 2J₂ cos 2θ + 2J₄ cos 4θ − ...
  sin(z cos θ) = 2J₁ cos θ − 2J₃ cos 3θ + 2J₅ cos 5θ − ...
  Bridges FM carrier decomposition, ROM harmonic phases, and optical frequency combs.
trigger:
  - phase-modulated sinusoidal signal → harmonic decomposition
  - ROM HHG: determining harmonic phase relative to fundamental
  - frequency comb: carrier-envelope offset from FM Bessel sidebands
reasoning_role: fm_bessel
parent: mathematics.plane_wave_spectrum
retrieval_cost: 1
---

# reasoning.mt.fm_bessel_expansion — Phase-Modulated Carrier → Harmonics

## Core Picture

A sinusoidal carrier with sinusoidal phase modulation:
```
E(t) = sin(ω t + β cos Ω t)
```
is exactly decomposable into discrete sidebands at frequencies ω ± n Ω via
Bessel functions of the first kind J_n(β). The modulation index β controls
the harmonic content. The phase of each sideband (sin vs cos) is determined
by the PRODUCT of the unmodulated carrier phase and the parity of the
modulation term. This is the Jacobi-Anger expansion.

## Derivation Sketch

### 1. Jacobi-Anger identity (the master formula)

The complex exponential form:
```
e^{i z cos θ} = Σ_{n=−∞}^{∞} i^n J_n(z) e^{i n θ}
              = J₀(z) + 2 Σ_{k=1}^{∞} i^k J_k(z) cos(k θ)
```

Separation into real and imaginary parts yields the two workhorse identities:
```
cos(z cos θ) = J₀(z) + 2 Σ_{k=1}^{∞} (−1)^k J_{2k}(z) cos(2k θ)
sin(z cos θ) = 2 Σ_{k=0}^{∞} (−1)^k J_{2k+1}(z) cos((2k+1) θ)
```

Key property: cos(z cos θ) is purely even → only EVEN-order Bessel functions.
sin(z cos θ) is purely odd → only ODD-order Bessel functions.

### 2. FM signal decomposition — the operational form

For a carrier at frequency ω modulated at frequency Ω with index β:
```
E(t) = sin(ω t + β cos Ω t)
```

Using sin(A+B) = sin A cos B + cos A sin B:
```
E(t) = sin(ω t) cos(β cos Ω t) + cos(ω t) sin(β cos Ω t)
```

Substituting the Jacobi-Anger identities above:

**Line 1** — sin(ωt) × cos(β cos Ωt):
```
sin(ωt) · [J₀ + 2 Σ_{k=1} (−1)^k J_{2k} cos(2k Ω t)]
= J₀ sin(ωt) + Σ_{k=1} (−1)^k J_{2k} [sin(ω+2kΩ)t + sin(ω−2kΩ)t]
```
These are the EVEN-order sidebands: ω ± 2Ω, ω ± 4Ω, ... — all with sin phase.

**Line 2** — cos(ωt) × sin(β cos Ωt):
```
cos(ωt) · [2 Σ_{k=0} (−1)^k J_{2k+1} cos((2k+1) Ω t)]
= Σ_{k=0} (−1)^k J_{2k+1} [cos(ω+(2k+1)Ω)t + cos(ω−(2k+1)Ω)t]
```
These are the ODD-order sidebands: ω ± Ω, ω ± 3Ω, ... — all with cos phase.

### 3. The full assembled decomposition

```
sin(ωt + β cos Ωt) =

     J₀(β) sin(ωt)                              ← fundamental, sin phase
   + J₁(β) [cos(ω+Ω)t + cos(ω−Ω)t]              ← 1st sidebands, cos phase
   − J₂(β) [sin(ω+2Ω)t + sin(ω−2Ω)t]            ← 2nd sidebands, sin phase
   − J₃(β) [cos(ω+3Ω)t + cos(ω−3Ω)t]            ← 3rd sidebands, cos phase
   + J₄(β) [sin(ω+4Ω)t + sin(ω−4Ω)t]            ← 4th sidebands, sin phase
   + ...
```

**The π/2 phase shift**: the fundamental (sin ωt) and the odd harmonics (cos ωt)
differ by π/2. The fundamental peaks at ωt = π/2, while the first sidebands
(∝ J₁ cos ωt at k=0, n=1 for ω−Ω ≈ ω when Ω≪ω) peak at ωt = 0. This is the
mathematical origin of the HHG pulse appearing at the zero-crossing of the
fundamental.

### 4. Bessel function asymptotics for small β

For weak phase modulation (β ≪ 1):
```
J₀(β) ≈ 1 − β²/4        → fundamental essentially unchanged
J₁(β) ≈ β/2              → linear growth of 1st sidebands
J_n(β) ≈ (β/2)^n / n!    → rapid decay with n
```

The sideband content is controlled by β: for ROM HHG, β = 2ω₀ X_max/c ∼ a₀²
(the relativistic Doppler shift from critical surface oscillation).

### 5. Connection to optical frequency combs

For a mode-locked laser, the carrier-envelope offset frequency f_CEO arises
because the group and phase velocities differ inside the cavity. In terms of
the FM expansion: each comb line at ν_n = n f_rep + f_CEO can be written as
a carrier at n f_rep with a phase modulation at f_CEO. The Jacobi-Anger
expansion gives the same sideband structure — the f-2f interferometer works
by beating the J₁ sideband of the n-th line with the J₀ carrier of the 2n-th
line.

## Algorithm — Given (ω, Ω, β) → harmonic table

```
1. Compute J_n(β) for n = 0,1,2,... (Bessel function recurrence or lookup).
2. Carrier = J₀(β) sin(ωt).
3. For each n ≥ 1:
   - n odd:  (−1)^{(n−1)/2} J_n(β) [cos(ω+nΩ)t + cos(ω−nΩ)t]  ← cos phase
   - n even: (−1)^{n/2} J_n(β) [sin(ω+nΩ)t + sin(ω−nΩ)t]       ← sin phase
4. Phase shift between fundamental and nth harmonic:
   n odd → π/2, n even → 0 (relative to fundamental).
```

## Edge Cases

- **Large modulation (β > 1)**: the fundamental J₀(β) crosses zero at β ≈ 2.4048
  (first Bessel zero). At this point, ALL power is in the sidebands — the
  fundamental is extinguished. Relevant for ROM at extreme intensities.
- **PM vs FM**: the above is for Phase Modulation. For Frequency Modulation
  (cos(ωt + β sin Ωt)), the roles of Bessel orders swap (odd ↔ even parity
  flips). FM arises from Doppler shift in relativistic mirrors, PM from
  displacement modulation.

## Cross-References

- Abramowitz & Stegun, *Handbook of Mathematical Functions*, Ch.9 (Bessel functions)
- Arfken §11 (Bessel functions, generating functions, Jacobi-Anger)
- mathematics-theorems: mathematics.plane_wave_spectrum (parent — spectral decomposition)
- electrodynamics: reasoning.em.synchrotron_fourier_decomposition (same Bessel structure, synchrotron)
- ultrafast-optics: reasoning.uo.frequency_comb (f_CEO ↔ FM sideband interpretation)
- laser-plasma: reasoning.lp.laser_absorption_mechanisms (ROM phase modulation)
