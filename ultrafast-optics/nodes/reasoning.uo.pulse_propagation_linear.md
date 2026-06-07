---
skill_id: reasoning.uo.pulse_propagation_linear
type: reasoning
summary_50t: >
  Spectral phase ψ(ω)=ψ₀+ψ₁Δω+(ψ₂/2)Δω²+(ψ₃/6)Δω³+... with ψ_n=−β_nL.
  ψ₁→group delay τ_g=L/v_g. ψ₂→GDD→linear chirp and pulse broadening
  τ_out=τ_in√(1+(4ln2·ψ₂/τ_in²)²). ψ₃→TOD→asymmetric ringing. Transform
  limit: Gaussian τ_pΔν=0.44, sech² τ_pΔν=0.315. Fiber D=−(2πc/λ²)β₂.
  Material: ψ₂=−(λ³L/2πc²)d²n/dλ².
trigger:
  - computing how dispersion broadens/chirps an ultrashort pulse
  - designing dispersion for pulse stretching/compression
  - understanding the frequency-dependence of group delay
reasoning_role: linear_pulse_propagation
parent: reasoning.optics.pulse_propagation_nlse
retrieval_cost: 1
sign_convention: >
  Time convention e^{−iωt}. Spectral phase ψ(ω) = arg{E(ω)}.
  GDD = ψ₂ = d²ψ/dω² (fs²). Positive ψ₂ → positive chirp (red leads blue,
  instantaneous frequency increases with time). β₂ = −ψ₂/L for bulk medium.
  In fibers: D (ps/nm/km) = −(2πc/λ²)β₂. Normal dispersion: D<0, β₂>0.
  Anomalous dispersion: D>0, β₂<0. τ_p = FWHM of |a(t)|².
  Transform limit τ_p Δν: Gaussian 0.44, sech² 0.315.
references:
  - optics: reasoning.optics.pulse_propagation_nlse (parent — NLSE with β₂ term)
  - mathematics-theorems: mathematics.distribution_limits (Fourier transform pairs)
---

# reasoning.uo.pulse_propagation_linear — Spectral Phase → Chirp → Broadening

## Core Picture

An ultrashort pulse is defined by its complex spectral amplitude E(ω) = |E(ω)|e^{iψ(ω)}.
The spectral phase ψ(ω) completely determines the temporal shape through Fourier
transform. Linear propagation through a dispersive medium adds phase ψ(ω) = −β(ω)L
where β(ω) = ω n(ω)/c. The Taylor expansion of ψ(ω) around the carrier frequency
ω₀ reveals the hierarchy of dispersion effects (Weiner §4.1; Diels-Rudolph §1).

## Derivation Sketch

### 1. Spectral phase expansion

For a dispersive medium of length L, the propagation constant expanded around ω₀:
```
β(ω) = β₀ + β₁(ω−ω₀) + (β₂/2)(ω−ω₀)² + (β₃/6)(ω−ω₀)³ + ...
     where β_n = ∂ⁿβ/∂ωⁿ|_{ω₀}
```

The spectral phase accumulated is ψ(ω) = −β(ω)L, giving:
```
ψ(ω) = ψ₀ + ψ₁(ω−ω₀) + (ψ₂/2)(ω−ω₀)² + (ψ₃/6)(ω−ω₀)³ + ...
     where ψ_n = −β_n L
```

### 2. Physical meaning of each term (Weiner §4.1, eqs 4.3-4.22)

| Order | Name | Symbol | Effect |
|-------|------|--------|--------|
| ψ₀ | Absolute phase | −β₀L | Carrier phase; irrelevant for intensity |
| ψ₁ | Group delay | τ_g = L/v_g | Pulse delay; no shape change |
| ψ₂ | GDD (Group Delay Dispersion) | d²ψ/dω² | Linear chirp + symmetric broadening |
| ψ₃ | TOD (Third-Order Dispersion) | d³ψ/dω³ | Asymmetric distortion + ringing |

### 3. Group velocity and delay

From β₁ = ∂β/∂ω:
```
v_g = β₁⁻¹ = c/(n + ω dn/dω) = c/(n − λ dn/dλ)       (Weiner eq 4.12, 4.14)
τ_g = ψ₁ = L/v_g = β₁L                                   (group delay)
```

### 4. Group Delay Dispersion — pulse broadening and chirp

**GDD definition**:
```
GDD = ψ₂ = d²ψ/dω² = −β₂L    (units: fs²)
```

**Material GDD** (Weiner eq 4.21):
```
ψ₂ = −(λ³L)/(2πc²) · d²n/dλ²
```
Fused silica at 800 nm: d²n/dλ² > 0 → ψ₂ > 0 (normal dispersion). Typical:
ψ₂ ≈ +360 fs² per cm.

**Fiber dispersion parameter D** (Weiner eq 4.20):
```
D = ∂(v_g⁻¹)/∂λ = −(2πc/λ²)β₂      (units: ps/(nm·km))
```
Normal dispersion: D < 0, β₂ > 0. Anomalous: D > 0, β₂ < 0.

**Gaussian pulse broadening** (Weiner eq 4.23-4.24):
For an initially unchirped Gaussian pulse |a(t)|² = exp(−2t²/τ_p²) with
FWHM τ_p (τ_p² = 2τ₀²):
```
τ_out = τ_in √(1 + (4 ln 2 · ψ₂ / τ_in²)²)
```
The chirp parameter: a_out(t) acquires phase ∝ t² with chirp rate C.

**Physical picture of chirp**: GDD > 0 means lower frequencies (red) experience
less group delay → arrive earlier. Higher frequencies (blue) delayed more →
arrive later. Instantaneous frequency sweeps from low to high: positive chirp.

### 5. Third-Order Dispersion — asymmetric distortion

TOD produces oscillatory ringing on the LEADING edge for ψ₃ > 0 (normal β₃)
and on the TRAILING edge for ψ₃ < 0. The asymmetry cannot be compensated by
GDD alone. TOD becomes significant when:
```
|ψ₃| / τ_p³ ≳ 0.1       (rough criterion)
```
For fused silica at 800 nm: ψ₃ ≈ +27 fs³ per mm (Weiner eq 4.22).

### 6. Transform limit

The shortest possible pulse for a given spectral bandwidth Δν (FWHM) is the
transform-limited (TL) pulse where ψ(ω) = const:
```
τ_p · Δν = constant    (transform-limited time-bandwidth product)
Gaussian: τ_p Δν = 0.44    (≈ 2 ln 2 / π)
sech²:    τ_p Δν = 0.315
```

Any non-zero ψ₂ or higher phase terms broaden the pulse beyond the TL.

## Algorithm — Given Pulse + Medium → Output Pulse

```
1. INPUT: a_in(t) or E_in(ω), medium n(λ) or β(ω), length L.

2. COMPUTE SPECTRAL PHASE:
   For bulk medium: ψ(ω) = −(ω n(ω)/c) L.
   Expand around ω₀: compute ψ₁, ψ₂, ψ₃ via derivatives of n(ω).

3. FOURIER PROPAGATION:
   E_out(ω) = E_in(ω) · exp(i ψ(ω))
   a_out(t) = (1/2π) ∫ E_out(ω) e^{i(ω−ω₀)t} dω

4. ANALYTIC APPROXIMATION (Gaussian input, pure GDD):
   τ_out = τ_in √(1 + (4 ln 2 · ψ₂ / τ_in²)²).
   Chirp: instantaneous frequency ω_inst(t) = ω₀ + (2 ψ₂/(τ_in⁴+4ψ₂²)) t.

5. BROADENING RATIO (general):
   For τ_in ≪ √|ψ₂|: τ_out ≈ (4 ln 2)|ψ₂|/τ_in → far-field regime,
   output pulse duration ∝ bandwidth (time-domain Fraunhofer).

6. CHECK TOD: if |ψ₃|/τ_p³ > 0.1, full Fourier propagation needed.
```

## Edge Cases

- **Far-field broadening** (ψ₂ ≫ τ_in²): output pulse is the Fourier transform
  of the input spectrum — temporal shape directly mirrors spectral shape.
  This is the principle of pulse stretching in CPA.
- **Zero-dispersion wavelength**: λ_ZDW where d²n/dλ² = 0 → ψ₂ = 0.
  TOD dominates. Fused silica ZDW ≈ 1.27 μm.
- **Super-Gaussian spectra**: sharper spectral edges → stronger TOD ringing.
- **Material resonances**: n(ω) changes rapidly near absorption lines →
  breakdown of Taylor expansion; use full Sellmeier or Kramers-Kronig.

## Cross-References

- Weiner §4.1-4.3, Diels-Rudolph §1-2
- optics: reasoning.optics.pulse_propagation_nlse (parent — NLSE uses β₂ as input)
- ultrafast-optics: reasoning.uo.dispersion_compensation (GDD is what we compensate)
- electrodynamics: reasoning.em.optical_coherence (transform limit = coherence time)
