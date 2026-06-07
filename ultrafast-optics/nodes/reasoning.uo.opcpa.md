---
skill_id: reasoning.uo.opcpa
type: reasoning
summary_50t: >
  OPCPA = CPA + OPA: pump (ps-ns, high energy) + chirped signal (stretched
  fs seed) → χ⁽²⁾ parametric amplification in nonlinear crystal. Phase
  matching: Δk = k_p−k_s−k_i = 0. Non-collinear (NOPA) → ultra-broadband
  (Δλ > 200 nm, τ < 10 fs). Idler carries unused energy. Contrast: no ASE,
  lower B-integral than CPA. Key: temporal overlap pump-signal, crystal
  damage threshold.
trigger:
  - designing few-cycle, high-contrast, high-energy laser systems
  - choosing between OPCPA and CPA for a given wavelength/pulse-width regime
  - computing parametric gain bandwidth from phase-matching geometry
reasoning_role: opcpa_design
parent: reasoning.uo.chirped_pulse_amplification
retrieval_cost: 1
sign_convention: >
  Type I: signal+idler same polarization ⊥ pump. Type II: signal⊥idler.
  Non-collinear angle α between pump and signal. Phase-matching:
  k_p = k_s + k_i (vector). Parametric gain G = ¼ exp(2ΓL) for ΓL ≫ 1.
  Γ² = (2ω_s ω_i d_eff² I_p)/(n_s n_i n_p ε₀ c³). d_eff from crystal symmetry.
references:
  - ultrafast-optics: reasoning.uo.chirped_pulse_amplification (sibling)
  - electrodynamics: reasoning.em.nonlinear_optical_response (χ⁽²⁾ OPA)
---

# reasoning.uo.opcpa — Optical Parametric Chirped Pulse Amplification

## Core Picture

OPCPA replaces the laser gain medium (Ti:sapphire, Yb) with parametric
amplification in a χ⁽²⁾ nonlinear crystal. A high-energy, narrow-band pump
pulse (ps-ns duration) amplifies a chirped broadband signal (stretched fs
seed) via three-wave mixing: pump → signal + idler. The key advantage over
CPA: parametric gain has NO energy storage → no ASE, no thermal lensing,
and gain bandwidth set by phase-matching geometry rather than atomic
transitions (Diels-Rudolph §7.6-7.8, Dubietis 1992).

## Derivation Sketch

### 1. Parametric amplification (from χ⁽²⁾ coupled-wave equations)

Signal growth in a non-depleted pump (undepleted pump approximation):
```
dA_s/dz = i (ω_s d_eff/(n_s c)) A_p A_i* e^{iΔk z}
```
For high gain (ΓL ≫ 1) with phase matching Δk = 0:
```
G = I_s(L)/I_s(0) ≈ ¼ exp(2ΓL)
Γ² = (2 ω_s ω_i d_eff² I_p) / (n_s n_i n_p ε₀ c³)
```
Gain scales EXPONENTIALLY with √(I_p) × L × d_eff.

### 2. Phase-matching and gain bandwidth

**Collinear phase matching**: k_p = k_s + k_i (scalar). For Type I BBO
pumped at 532 nm, signal at 800 nm: θ_pm ≈ 24°. Bandwidth Δλ ∼ 50 nm.

**Non-collinear OPA (NOPA)**: k_p, k_s, k_i form a triangle. The non-collinear
angle α between pump and signal flattens the phase-matching curve:
```
∂Δk/∂ω_s ≈ 0    over broad range → ultra-broadband gain
```
For BBO, α ≈ 2.3° (internal) gives Δλ > 200 nm at 800 nm → supports
sub-5-fs pulses. This is the "magic" of NOPA.

**Phase-matching types**:
- **Type I**: e→o+o (BBO). Signal and idler ordinary, pump extraordinary.
- **Type II**: e→e+o or e→o+e. Lower d_eff than Type I but sometimes
  broader bandwidth.

### 3. OPCPA architecture

```
Oscillator (fs, nJ) → stretcher (ps) → OPA stages (1-4) → compressor (fs)
                       ↑ pump laser (ps-ns, mJ-J, synchronized)
```

**Pump laser**: Typically frequency-doubled Nd:YAG (532 nm, ∼100 ps) or
Nd:YLF (527 nm). Must be synchronized to the seed pulse to <1 ps jitter.

**Multi-stage OPCPA**:
- Stage 1: low gain (∼10³), high beam quality. BBO, 1-2 mm.
- Stage 2: intermediate gain (∼10²-10³). BBO or LBO, 3-5 mm.
- Stage 3-4: power amplifiers. Larger crystals, higher pump energy.

**Pump depletion**: At high conversion efficiency (η > 10%), pump depletion
modifies the gain dynamics. Analytic solutions via Jacobi elliptic functions
(Armstrong 1962).

### 4. OPCPA advantages over CPA

| Property | CPA | OPCPA |
|----------|-----|-------|
| Gain bandwidth | Limited by atomic transition (Ti:S ∼ 100 THz) | Phase-matching design (NOPA >200 THz) |
| ASE / contrast | ASE pedestal (∼10⁻⁵-10⁻³ contrast) | No ASE (parametric, no stored energy) |
| Thermal load | High (quantum defect ∼35%) | Low (no absorption, quantum defect in idler) |
| B-integral | Accumulates through multi-pass | Lower (fewer passes, shorter path) |
| Wavelength | Fixed to gain media | Tunable by phase-matching angle/temperature |
| Complexity | Single pump laser | Two synchronized lasers (seed + pump) |

### 5. Contrast — the killer advantage

CPA has a nanosecond ASE pedestal from the amplifier's spontaneous emission
— problematic for laser-plasma experiments where pre-pulse >10¹⁰ W/cm²
ionizes the target before the main pulse arrives. OPCPA has ZERO ASE:
parametric gain only exists during the pump pulse (∼100 ps window).

**Contrast measurement**: Third-order autocorrelator (Sequoia) can measure
contrast to 10⁻¹². Typical OPCPA: >10¹⁰ contrast at ps timescales.

## Algorithm — Given Target → OPCPA Design

```
1. SPECIFY: λ_s (signal), τ_comp (compressed), E_out, f_rep.

2. SELECT CRYSTAL: BBO (high d_eff, UV pump), LBO (high damage threshold,
   IR pump), KDP/DKDP (large aperture, kJ-class). d_eff from crystal class.

3. PHASE MATCHING: Compute θ_pm, α (NOPA) for target λ_s.
   ∂Δk/∂ω_s = 0 → find α for broadband.
   Gain bandwidth Δλ = λ²/(c·τ_gvm) where τ_gvm is group-velocity mismatch.

4. PUMP: λ_p, τ_pump > τ_stretch (ensures full temporal overlap).
   I_p < I_damage (BBO: ∼10 GW/cm² at 532 nm, ns pulses).
   Synchronization jitter < 100 fs rms.

5. STAGES: Σ G_i = E_out/E_seed.
   B-integral per stage: B_i = (2π/λ) n₂ I(z) dz.
   Keep B_total < 1.5 for high-contrast systems.

6. COMPRESSOR: Same design as CPA (grating pair, matched GDD).
   Output: τ_comp, contrast, beam quality (M²).
```

## Cross-References

- Diels-Rudolph §7.6-7.8, Dubietis 1992 (OPCPA), Dubietis 2006 (NOPA)
- electrodynamics: reasoning.em.nonlinear_optical_response (χ⁽²⁾ parent)
- ultrafast-optics: reasoning.uo.chirped_pulse_amplification (sibling — CPA)
- ultrafast-optics: reasoning.uo.dispersion_compensation (compressor design)
- ultrafast-optics: knowledge.uo.ultrafast_amplifier_data (system parameters)
