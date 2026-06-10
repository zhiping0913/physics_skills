---
skill_id: reasoning.uo.chirped_pulse_amplification
type: reasoning
summary_50t: >
  CPA: stretch (GDD>0, ps-ns) → amplify (gain medium, avoid damage) →
  compress (GDD<0, back to fs). Stretcher: grating/grism/fiber (GDD∼10⁵-10⁶ fs²).
  B-integral: B = (2π/λ)∫ n₂I dz < π limits nonlinear phase. Gain narrowing:
  Δν_out = Δν_in/√(1+ln G₀·(Δν_in/Δν_g)²). Compressor: grating pair, matched
  GDD to stretcher. TOD-limited τ_comp ≈ τ_TL·√(1+(ψ₃,net/τ_TL³)²).
trigger:
  - designing CPA systems for mJ-PW peak power femtosecond pulses
  - computing B-integral and gain narrowing for a multi-stage amplifier
  - diagnosing compressed pulse quality limited by residual TOD
reasoning_role: cpa_amplifier_design
parent: reasoning.uo.dispersion_compensation
retrieval_cost: 1
sign_convention: >
  B = (2π/λ)∫₀^L n₂ I(z) dz. B < π: acceptable pulse quality.
  B ∼ 3-5: severe temporal/spectral distortion.
  Stretcher GDD > 0 (normal). Compressor GDD < 0 (anomalous).
  Strecher ratio = τ_stretched/τ_TL ≈ 10³-10⁴.
references:
  - ultrafast-optics: reasoning.uo.dispersion_compensation (parent — GDD management)
  - ultrafast-optics: reasoning.uo.pulse_propagation_nlse_higher_order (nonlinear propagation)
---

# reasoning.uo.chirped_pulse_amplification — Stretch → Amplify → Compress

## Core Picture

Chirped Pulse Amplification (CPA, Strickland & Mourou 1985) solves the
fundamental problem of femtosecond amplification: peak intensities at the
gain medium would cause catastrophic damage and nonlinear distortion.
By stretching the pulse in time by 10³-10⁴× before amplification and
recompressing afterward, CPA keeps the peak intensity below the damage
threshold while extracting energy from the gain medium. The enabling
insight: dispersion is reversible — what a grating stretcher disperses,
a matched grating compressor can undo (Weiner §11, Diels-Rudolph §7).

## Derivation Sketch

### 1. The damage problem and CPA solution

Without CPA: a 100 fs, 1 mJ pulse has P_peak ≈ 10 GW. Focused to 100 μm
diameter → I ≈ 10¹⁴ W/cm² → far above damage threshold of most optics
(∼10⁹-10¹⁰ W/cm² for coatings, ∼10¹¹ W/cm² for bulk crystals).

CPA stretches to τ_s ∼ 300 ps: P_peak drops by 3000× → I ∼ 3×10¹⁰ W/cm²
→ safe amplification. After amplification to 1 J, the compressor brings
it back to 300 fs → P_peak ∼ 3 TW.

### 2. Stretcher design

**Grating stretcher** (Martinez 1987): Telescope between gratings reverses
the sign of GDD compared to the compressor — gives POSITIVE GDD.
```
GDD_stretch ≈ +(λ³ L_eff)/(2πc² d² cos² θ_d)    [positive, large]
TOD_stretch ≈ positive (same sign as material)
```

**Alternative stretchers**:
- **Fiber stretcher**: Long fiber (∼km SMF) with normal GDD. Chromatic
  for broadband pulses.
- **Chirped fiber Bragg grating (CFBG)**: Compact, alignment-free. TOD
  from grating apodization.
- **Öffner triplet stretcher**: All-reflective, achromatic, large bandwidth.
  Standard in high-energy CPA.

**Stretcher ratio**: R = τ_s/τ_TL, typical R = 10³-10⁴.

### 3. Amplification — gain narrowing and B-integral

**Gain narrowing**: The finite gain bandwidth Δν_g reshapes the stretched
pulse spectrum. After amplification with total gain G₀:
```
Δν_out = Δν_in / √(1 + ln G₀ · (Δν_in/Δν_g)²)
```
For Ti:sapphire (Δν_g ≈ 100 THz, G₀ ≈ 10⁶): gain narrowing reduces 100 THz
→ ∼50 THz → limits compressed pulse to ∼20 fs.

**B-integral** — accumulated nonlinear phase:
```
B = (2π/λ) ∫₀^L n₂ I(z) dz
```
B measures the nonlinear phase accumulated per pass. When B > π, self-phase
modulation and self-focusing severely degrade the pulse:
- B < 1: negligible degradation
- 1 < B < 3: acceptable with minor pre-compensation
- B > 5: severe temporal/spectral breakup

B-integral is the design constraint that sets the stretcher ratio and
amplifier staging.

### 4. Multi-stage amplifier architecture

```
Oscillator → stretcher → preamp (μJ) → regen amp (mJ) → power amp (J)
   10 nJ       300 ps      1 μJ          5 mJ             1 J
   B∼0         B∼0.1       B∼0.5         B∼1.5            B∼2-3
```

**Regenerative amplifier**: Pulse trapped in cavity for ∼10-30 round-trips
through Ti:sapphire, pumped at 532 nm, 1 kHz. Pockels cell switches pulse
in/out. Gain ∼10⁶.

**Multi-pass amplifier**: 4-8 passes through cryo-cooled Ti:sapphire.
Higher energy extraction efficiency, lower gain per pass → less ASE.

### 5. Compressor — GDD matching

For a grating compressor to exactly undo the stretcher:
```
GDD_compress = −GDD_stretch
TOD_compress = ? — ideally opposite sign, but for grating pairs:
TOD_compress = −(3λ/2πc) (1+λ sin θ_d/(d cos² θ_d)) · GDD_compress
```
Both grating stretcher and compressor have TOD of the SAME sign →
TOD ADDS rather than cancels → net TOD limits pulse duration.

**Compressor alignment**:
- Grating parallelism: <0.1 mrad for sub-30 fs.
- Beam pointing: angular chirp from misalignment → spatial chirp.
- Double-pass: corner cube returns beam to grating for second pass.

### 6. Compressed pulse quality

**TOD-limited pulse** (Gaussian):
```
τ_comp = τ_TL · √(1 + (ψ₃,net / τ_TL³)²)
```
For Ti:sapphire CPA: typical τ_comp ≈ 25-30 fs (TOD-limited).

**ACP (Acousto-optic Programmable dispersive filter, "Dazzler"):**
Arbitrary spectral phase filter using collinear acousto-optic interaction.
Can pre-compensate TOD and higher-order phase → τ_comp < 20 fs.

## Algorithm — Given Target → CPA Design

```
1. SPECIFY target: E_out, τ_comp, λ₀, f_rep.

2. DAMAGE CONSTRAINT:
   I_max,stretched < I_damage → stretcher ratio R > (E_out/τ_TL)/(I_dam·A_eff).
   For Ti:sapphire: I_dam ∼ 10¹¹ W/cm² bulk, 10⁹ W/cm² coatings.
   R ≈ τ_TL/(E_out/(I_dam·A_eff)) ∼ 10³-10⁴ typical.

3. STRETCHER: Select grating (d, θ_d) and L_g to achieve GDD = R·τ_TL²/(4 ln 2).
   For 100 fs → 300 ps: GDD ≈ 5×10⁶ fs².

4. B-INTEGRAL BUDGET:
   Compute n₂I(z) through each amplifier stage.
   If B_total > 3: increase R, expand beam, or add relay imaging.

5. GAIN NARROWING: compute Δν_out from gain per stage.
   If Δν_out/Δν_TL < 1.5: needs broader gain medium or spectral shaping.

6. COMPRESSOR: Match grating to stretcher. Compute net TOD.
   If ψ₃,net/τ_TL³ > 0.1: add Dazzler or grism for TOD compensation.

7. OUTPUT: τ_comp, P_peak = 0.88 E_out/τ_comp (sech²), Strehl ratio.
```

### Gain saturation fundamentals (Principles of Lasers 2010, Ch.2,5-6)

The amplifier stages in CPA rely on stimulated emission from a population-
inverted gain medium. Key physics:

**Small-signal gain** (unsaturated, I ≪ I_sat):
```
I(z) = I₀ exp(g₀ z),    g₀ = σ ΔN₀    [cm⁻¹]
```
where σ is the stimulated emission cross-section and ΔN₀ = N₂ − (g₂/g₁)N₁
is the initial population inversion density.

**Gain saturation** (I ∼ I_sat):
```
dI/dz = g₀ I / (1 + I/I_sat),    I_sat = hν / (σ τ_f)
```
where τ_f is the fluorescence lifetime of the upper laser level. When
I ≫ I_sat, the gain is "bleached" and the extraction efficiency approaches
ΔN₀ hν per unit volume.

**Three-level vs four-level lasers** (Principles of Lasers Ch.1,6):
- **Three-level** (e.g., ruby, Er:fiber): the lower laser level IS the
  ground state → > 50% of active ions must be pumped to reach transparency.
  High threshold, low efficiency.
- **Four-level** (e.g., Nd:glass, Ti:sapphire, Yb:doped): the lower laser
  level is an excited state that rapidly decays → transparency at near-zero
  pump power. Low threshold, high efficiency. All CPA systems use four-level
  gain media.

**Ti:sapphire specifics** (σ ≈ 3×10⁻¹⁹ cm² at 800 nm, τ_f ≈ 3.2 μs,
I_sat ≈ 0.9 J/cm² for 100 fs stretched pulse, Δλ_gain ≈ 650–1100 nm).

## Cross-References

- Weiner §11, Diels-Rudolph §7, Strickland & Mourou 1985
- ultrafast-optics: reasoning.uo.dispersion_compensation (parent — GDD/TOD)
- ultrafast-optics: reasoning.uo.pulse_propagation_nlse_higher_order (B-integral physics)
- ultrafast-optics: reasoning.uo.opcpa (alternative amplification)
- ultrafast-optics: knowledge.uo.ultrafast_amplifier_data (typical system parameters)
