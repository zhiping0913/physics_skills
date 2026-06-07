---
skill_id: reasoning.uo.pulse_propagation_nlse_higher_order
type: reasoning
summary_50t: >
  Generalized NLSE: ∂A/∂z = −(α/2)A − i(β₂/2)∂²A/∂T² + (β₃/6)∂³A/∂T³
  + iγ[|A|²A + (i/ω₀)∂(|A|²A)/∂T − T_R A ∂|A|²/∂T]. Terms: GVD, TOD,
  SPM, self-steepening (shock formation at few-cycle), stimulated Raman
  scattering (soliton self-frequency shift). Cross-domain: same equation
  structure governs fiber solitons, filamentation, supercontinuum.
trigger:
  - modeling few-cycle pulse propagation where NLSE assumptions break down
  - explaining supercontinuum generation or soliton self-frequency shift
  - analyzing pulse dynamics near zero-dispersion wavelength
reasoning_role: generalized_nlse_solver
parent: reasoning.optics.pulse_propagation_nlse
retrieval_cost: 1
sign_convention: >
  Retarded time T = t − z/v_g. β₂>0: normal GVD. β₂<0: anomalous.
  γ = ω₀ n₂/(c A_eff) > 0 for self-focusing Kerr media. Self-steepening
  term: ∂(|A|²A)/∂T (time derivative of SPM). Raman: T_R ≈ 1-5 fs for
  silica (fractional Raman contribution f_R ≈ 0.18). Shock formation
  distance: z_shock ∝ τ_in/(n₂ I₀).
references:
  - optics: reasoning.optics.pulse_propagation_nlse (parent — standard NLSE)
  - electrodynamics: reasoning.em.nonlinear_optical_response (χ⁽³⁾ origin of γ, n₂)
---

# reasoning.uo.pulse_propagation_nlse_higher_order — Beyond Standard NLSE

## Core Picture

The standard NLSE (∂A/∂z = −i(β₂/2)∂²A/∂T² + iγ|A|²A) assumes:
slowly-varying envelope, instantaneous nonlinearity, and dominant GVD.
For pulses shorter than ~100 fs or near the zero-dispersion wavelength, these
assumptions fail. The **generalized NLSE** (GNLSE) adds TOD, self-steepening,
and delayed Raman response — the three corrections that govern few-cycle
pulse dynamics, supercontinuum generation, and soliton self-frequency shift
(Weiner §5, Diels-Rudolph §5, Agrawal §2).

## Derivation Sketch (from standard NLSE → GNLSE)

Starting from `reasoning.optics.pulse_propagation_nlse` (standard NLSE):

### 1. The generalized NLSE (Agrawal eq 2.3.36; Weiner §5.4)

```
∂A/∂z = −(α/2) A                     [linear loss]
        − i(β₂/2) ∂²A/∂T²            [GVD]
        + (β₃/6) ∂³A/∂T³             [TOD]
        + iγ |A|² A                    [SPM — Kerr nonlinearity]
        − (γ/ω₀) ∂(|A|²A)/∂T          [self-steepening — ∝ 1/ω₀]
        + iγ T_R A ∂|A|²/∂T           [stimulated Raman scattering]
```

All terms evaluated in the retarded time frame T = t − z/v_g.

### 2. Self-steepening — shock formation (Weiner §5.3)

**Physical origin**: The group velocity depends on intensity through the
nonlinear refractive index: v_g(I) = v_g₀/(1 + n₂I). The peak of the pulse
travels slower than the wings → the trailing edge steepens. At few-cycle
durations, this forms an optical shock.

**Mathematical form**: The term −(γ/ω₀) ∂(|A|²A)/∂T is the first-order
correction from the frequency dependence of the nonlinearity. It arises
from the full Maxwell wave equation for the envelope beyond the SVEA:
```
∇²E − (1/c²) ∂²[(1+χ⁽³⁾|E|²)E]/∂t² = 0
```
The time derivative on the nonlinear polarization produces the ∂/∂T term.

**Shock distance** (Agrawal §4.4): the self-steepening compresses the trailing
edge until a gradient catastrophe occurs at:
```
z_shock ≈ 0.43 τ_in / (γ P₀)   (for sech² pulse)
```

**Critical regime**: z_shock ∼ L_D (dispersion length) when τ_p ∼ 5-10 fs.
For Ti:sapphire oscillators (τ_p ∼ 100 fs): self-steepening negligible.
For few-cycle pulses (τ_p < 10 fs): dominant.

### 3. Stimulated Raman scattering — soliton self-frequency shift (Weiner §5.4)

**Physical origin**: The electronic Kerr response is NOT instantaneous.
The nuclear contribution (molecular vibrations) responds with a delayed
response function h_R(t) with characteristic time T_R ∼ 1-5 fs in silica.
The fractional Raman contribution f_R ≈ 0.18 (82% instantaneous electronic,
18% delayed nuclear).

**Raman response function** (Agrawal §2.3):
```
R(t) = (1−f_R) δ(t) + f_R h_R(t)
h_R(t) = (τ₁²+τ₂²)/(τ₁τ₂²) exp(−t/τ₂) sin(t/τ₁)   (τ₁≈12.2 fs, τ₂≈32 fs for silica)
```

**Raman term in GNLSE**: iγ T_R A ∂|A|²/∂T, where T_R = ∫₀^∞ t h_R(t) dt
is the first moment of the Raman response.

**Soliton self-frequency shift (SSFS)**: A soliton in anomalous dispersion
continuously shifts to LONGER wavelengths (lower frequencies) via intrapulse
Raman scattering. The shift rate:
```
dν₀/dz ∝ −|β₂|/τ_p⁴   (stronger shift for shorter pulses)
```
This is the primary mechanism limiting soliton-based communications and the
engine behind supercontinuum generation in photonic crystal fibers.

### 4. TOD — dispersion-wave generation (Weiner §4.4)

When β₃ ≠ 0, a soliton in anomalous dispersion can phase-match to a linear
**dispersive wave** in the normal dispersion regime. The phase-matching
condition determines the resonant frequency:
```
β(ω_dw) − β(ω_s) − (ω_dw−ω_s)/v_g,s − γP_s/2 = 0
```
This Cherenkov-like radiation process generates narrow-band spectral peaks
that are prominent in supercontinuum spectra.

## Algorithm — Given Pulse + Fiber → Output After Propagation

```
1. INPUT: A(0,T), fiber parameters (β₂,β₃,γ,α, T_R, f_R).
   Optional: higher-order β₄,β₅ for ultra-broadband (>100 THz).

2. CHOOSE NUMERICAL METHOD:
   - Split-step Fourier (SSF): handle dispersion in ω-domain,
     nonlinearity in t-domain. Simple, O(N log N).
   - Fourth-order Runge-Kutta in interaction picture (RK4IP):
     more accurate for few-cycle pulses.
   - For supercontinuum: adaptive step size, Raman convolution.

3. DISPERSION STEP (ω-domain):
   Ã(z+Δz/2, ω) = Ã(z,ω) · exp[−i(β₂ω²/2+β₃ω³/6+...)Δz/2]

4. NONLINEAR STEP (t-domain):
   Include SPM, self-steepening, Raman:
   ∂A/∂z|_{NL} = iγ[|A|²A + (i/ω₀)∂(|A|²A)/∂T − T_R A ∂|A|²/∂T]

5. COMPUTE DIAGNOSTICS:
   - Temporal: |A(z,T)|², instantaneous frequency ω_inst(T)
   - Spectral: |Ã(z,ω)|² (dB scale for supercontinuum)
   - Energy: check conservation (loss only from α)
   - Coherence: g₁₂(ω) for supercontinuum noise properties

6. IDENTIFY FEATURES:
   - Soliton fission → N solitons + dispersive waves
   - SSFS → long-wavelength shift of fundamental soliton
   - Shock → steepened trailing edge, spectral broadening to blue
```

## Cross-Domain Connections

| Domain | Equation | Higher-order terms |
|--------|----------|-------------------|
| Fiber optics | GNLSE | β₃, self-steepening, Raman (T_R∼1-5 fs) |
| Bulk filamentation | (3+1)D NLSE | Diffraction + plasma defocusing + MPA |
| Water waves | Dysthe equation | 4th-order dispersion, nonlinear dispersion |
| Plasma wakes | Envelope equation | Relativistic self-steepening, wakefield |
| Bose-Einstein condensates | Gross-Pitaevskii | 3-body recombination |

**Plasma connection**: In laser-plasma interaction, the relativistic mass
increase produces a nonlinearity analogous to self-steepening — the
effective plasma frequency ω_p/√γ shifts with intensity. Cross-reference:
`plasma: reasoning.plasma.laser_plasma_interaction`.

## Edge Cases

- **Zero-dispersion wavelength (ZDW)**: β₂ ≈ 0 → TOD dominates.
  Supercontinuum generation relies on pumping near ZDW.
- **Self-focusing critical power**: When P > P_cr, the Kerr lens overcomes
  diffraction, causing beam collapse. The critical power:
  ```
  P_cr = α λ²/(4π n₀ n₂)
  ```
  where α depends on beam profile: Townes (optimal self-trapping) α≈1.86,
  Gaussian (aberrationless) α≈1.86. For Ti:sapphire at 800 nm (n₀≈1.76,
  n₂≈3×10⁻¹⁶ cm²/W): P_cr ≈ 2.6 MW. Self-focusing distance:
  ```
  z_sf = L_diff / √(P/P_cr − 1)     (Marburger/Akhmanov)
  ```
  where L_diff = k₀ w₀² is the Rayleigh length. For P close to P_cr,
  z_sf → ∞ (stable self-trapping for Townes profile). Above P_cr, beam
  collapses at finite z_sf. In filamentation, plasma defocusing balances
  Kerr at I_clamp ≈ few×10¹³ W/cm² in air.
- **Raman response in gases**: T_R ∼ 100-300 fs (molecular rotation),
  much longer than in solids. Enables coherent rotational Raman generation.
- **Plasma contribution**: Above the ionization threshold (∼10¹³ W/cm²),
  free-electron plasma contributes negative GVD (∝ −ω_p²/ω³) and
  defocusing nonlinearity. Essential for filamentation modeling.
- **Carrier-envelope phase effects**: For τ_p < 2 optical cycles,
  the CEP φ_CEO influences the peak field → the pulse is no longer
  fully described by the envelope alone. The GNLSE breaks down;
  use the full Maxwell solver or the carrier-resolved unidirectional
  pulse propagation equation (UPPE).

## Cross-References

- Weiner §5.3-5.4, Diels-Rudolph §5, Agrawal §2.3, §4-5
- optics: reasoning.optics.pulse_propagation_nlse (parent — standard NLSE)
- electrodynamics: reasoning.em.nonlinear_optical_response (Kerr n₂, Raman gain)
- ultrafast-optics: reasoning.uo.pulse_propagation_linear (β₂, β₃ from dispersion)
- plasma: reasoning.plasma.laser_plasma_interaction (relativistic self-steepening analog)
