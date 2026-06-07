---
skill_id: reasoning.uo.dispersion_compensation
type: reasoning
summary_50t: >
  Compensate GDD and TOD to maintain/restore ultrashort pulses. Prism pair
  (Fork 1984): GDD∝−L_sep, TOD remnant. Grating pair (Treacy 1969):
  GDD = −(λ³L_g)/(2πc²d² cos²θ_d). Chirped mirror (Szipöcs 1994):
  λ-dependent penetration depth → flat GDD over octave. Gires-Tournois
  interferometer: resonant GDD∝finesse. CPA: stretcher GDD>0 + compressor
  GDD<0 → near-zero net GDD, residual TOD limits pulse duration.
trigger:
  - designing stretcher/compressor for CPA systems
  - choosing dispersion compensation elements for a mode-locked laser cavity
  - estimating residual TOD-limited pulse duration
reasoning_role: dispersion_compensation_design
parent: reasoning.uo.pulse_propagation_linear
retrieval_cost: 1
sign_convention: >
  GDD > 0: normal dispersion (material). GDD < 0: anomalous (gratings,
  prism pairs properly aligned). Grating: Littrow angle θ_d = arcsin(λ/d).
  Double-pass doubles GDD. Net GDD = Σ GDD_i. TOD compensation requires
  matching ∂GDD/∂λ across elements.
references:
  - ultrafast-optics: reasoning.uo.pulse_propagation_linear (parent — GDD/TOD definitions)
---

# reasoning.uo.dispersion_compensation — Prism / Grating / Chirped Mirror → Flat GDD

## Core Picture

Ultrashort pulses accumulate material GDD ∼ 360 fs²/cm in fused silica at
800 nm. To generate and maintain femtosecond pulses, this positive GDD must
be compensated by elements providing **anomalous (negative) GDD**. Three
families of devices achieve this through angular dispersion (prisms, gratings)
or resonant structures (chirped mirrors, GTI). For CPA, the stretcher provides
large positive GDD; the compressor provides matching negative GDD, leaving
a residual dominated by TOD mismatch (Weiner §4.5-4.6, Diels-Rudolph §2).

## Derivation Sketch

### 1. Prism pair — angular dispersion → negative GDD (Fork 1984)

A sequence of four prisms (or two in double-pass) at Brewster angle provides
tunable negative GDD. The key physics: different wavelengths traverse different
path lengths through glass because the beam is angularly dispersed.

**Single-pass prism-pair GDD** (Weiner §4.5):
```
GDD_prism ≈ −(2λ³/πc²) (dn/dλ)² L_sep    [for θ = θ_Brewster]
```
where L_sep is the tip-to-tip prism separation. The GDD is always **negative**
and scales linearly with separation → tunable.

**Prism material figure of merit**: (dn/dλ)² determines GDD per unit length.
SF10 glass (high dispersion) gives ∼5× stronger GDD than fused silica.

**TOD from prism pair**: Typically positive TOD (opposite sign to grating
compressor). Can partially compensate grating TOD in CPA systems.

### 2. Grating pair — pure negative GDD (Treacy 1969)

A parallel grating pair in double-pass configuration:

**Grating equation**: d(sin θ_i + sin θ_d) = mλ

**Double-pass GDD** (Weiner eq 4.37):
```
GDD_grat = −(λ³ L_g) / (2π c² d² cos² θ_d)
```
where L_g is the perpendicular grating separation, d is the groove spacing
(typically 1/λ lines/mm), and θ_d is the diffracted angle.

**Key properties**:
- GDD is always NEGATIVE (anomalous)
- Scales ∝ 1/d² — denser grooves → stronger GDD
- Scales ∝ L_g — longer separation → stronger GDD
- No material dispersion → pure geometric effect, works at any wavelength

**Grating TOD**:
```
TOD_grat = −(3λ⁴ L_g)/(2π² c³ d² cos² θ_d) · (1 + λ sin θ_d/(d cos² θ_d))
```
Grating TOD is negative (same sign as GDD). Cannot be compensated by material
alone → limits CPA compressed pulse duration.

### 3. Chirped mirror — wavelength-dependent penetration (Szipöcs 1994)

A dielectric Bragg mirror where the layer thickness varies monotonically →
longer wavelengths penetrate deeper before being reflected.

**Design principle**: The Bragg wavelength of a layer pair d_i is λ_B ≈ 2n_eff d_i.
By varying d_i across the stack, each wavelength reflects at a different
physical depth z(λ).

**GDD from penetration depth** (Weiner §4.6.3):
```
GDD_CM(λ) = 2 · (2n/c) · dz/dλ
```
The factor 2 accounts for round-trip; dz/dλ is the slope of penetration
vs wavelength. A linearly chirped mirror (dz/dλ = const) gives flat GDD
over the design bandwidth.

**Figure of merit**: Octave-spanning chirped mirrors (600-1200 nm) with
|GDD| < 20 fs² ripple are commercially available. They are the enabling
technology for sub-6-fs Ti:sapphire oscillators.

**Double-chirped mirrors (DCM)** (Kärtner 1997): Add an antireflection
coating whose thickness is also chirped to suppress the impedance mismatch
at the ambient-mirror interface → reduced GDD oscillations.

### 4. Gires-Tournois interferometer (GTI)

A Fabry-Perot etalon with 100% back reflector → all incident light reflected,
but with wavelength-dependent phase:
```
φ(λ) = −2 arctan[ (1+√R)/(1−√R) · tan(2πnd cos θ/λ) ]
GDD_GTI = d²φ/dω²
```
Resonant GDD peaks at wavelengths satisfying the resonance condition.
The GDD magnitude ∝ finesse F = π√R/(1−R). Used for fine-tuning cavity
dispersion in mode-locked lasers.

### 5. CPA stretcher-compressor matching

In CPA (Chirped Pulse Amplification):
1. **Stretcher**: Material (positive GDD) or grating stretcher (positive
   GDD in telescope configuration) → stretches pulse to ∼100 ps−1 ns.
2. **Amplifier**: Gain medium adds material GDD (positive).
3. **Compressor**: Grating pair (negative GDD) → recompresses.

**Residual phase** after matched stretcher + compressor:
```
ψ_res(ω) ≈ (ψ₃,stretch − ψ₃,compress)(ω−ω₀)³/6 + ... (TOD-limited)
```
The compressed pulse duration, TOD-limited:
```
τ_comp ≈ τ_TL · [1 + (|ψ₃|/τ_TL³)²]^{1/2}    (for Gaussian)
```
Typical: ∼30 fs for Ti:sapphire CPA without TOD compensation.

## Algorithm — Given Required GDD → Select Elements

```
1. COMPUTE material GDD:
   Sum GDD_mat = Σ_i GDD_i × L_i over all transmissive elements.

2. COMPUTE net cavity GDD target:
   - Soliton mode-locking: small net anomalous GDD (∼−100 to −1000 fs²).
   - Stretched-pulse: alternating normal+anomalous per roundtrip.
   - CPA: stretcher GDD = −compressor GDD (after amplification).

3. SELECT compensators:
   - Tunable: prism pair (GDD ∝ −L_sep, tens to few 1000s fs²).
   - Large negative: grating pair (GDD ∝ L_g/d²).
   - Broadband flat: chirped mirror (fixed GDD, octave bandwidth).
   - Fine tuning: GTI (resonant, narrowband).

4. ADD contributions:
   GDD_net = GDD_mat + GDD_prisms + GDD_gratings + GDD_CM + GDD_GTI.
   Adjust L_sep or grating spacing to meet target.

5. CHECK TOD: compute net TOD. If |TOD_net|/τ_p³ > 0.1:
   - Add TOD compensation (grating + prism TOD have opposite signs).
   - Use grism (grating+prism hybrid) for simultaneous GDD/TOD control.
   - For CPA: acousto-optic programmable dispersive filter (AOPDF, Dazzler).

6. VERIFY: compute output pulse via Fourier propagation (R1 algorithm)
   with net ψ(ω). Check τ_out is within tolerance.
```

## Element Comparison Table

| Element | GDD sign | GDD range (fs²) | Bandwidth | TOD sign | Tunable |
|---------|---------|-----------------|-----------|----------|---------|
| Fused silica (1 cm) | + | +360 | Broad | + | No |
| SF10 prism pair (30 cm sep) | − | −500 to −5000 | Moderate | + | Yes (L_sep) |
| Grating pair (1200 l/mm, 10 cm) | − | −10⁴ to −10⁶ | Broad | − | Yes (L_g) |
| Chirped mirror (1 bounce) | − | −20 to −100 | Octave | Designed | No |
| GTI | ± | ±10 to ±500 | Narrow | ± | Yes (angle) |
| Grism (grating+prism) | − | −10³ to −10⁵ | Broad | 0 (matched) | Limited |

## Edge Cases

- **Over-compensation**: Net anomalous GDD for soliton mode-locking must stay
  within soliton existence range: 0 < |β₂,net| < β₂,crit.
- **Spatial chirp from prisms/grating**: Angular dispersion produces spatial
  separation of wavelengths. Double-pass or corner-cube retroreflector cancels
  this.
- **Third-order mismatch in CPA**: Grating stretcher and compressor have TOD
  of same sign → add up rather than cancel. Grism or Dazzler needed for
  < 20 fs compressed pulses.

## Cross-References

- Weiner §4.5-4.7, Diels-Rudolph §2, Siegman §9
- Fork 1984 (prism pair), Treacy 1969 (grating pair), Szipöcs 1994 (chirped mirror)
- ultrafast-optics: reasoning.uo.pulse_propagation_linear (parent — ψ₂,ψ₃ definitions)
- ultrafast-optics: reasoning.uo.chirped_pulse_amplification (CPA stretcher/compressor)
- ultrafast-optics: knowledge.uo.dispersion_data (material GDD values)
