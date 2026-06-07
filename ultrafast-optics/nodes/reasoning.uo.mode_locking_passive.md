---
skill_id: reasoning.uo.mode_locking_passive
type: reasoning
summary_50t: >
  Passive mode-locking via saturable absorber (SA). Fast SA (τ_A ≪ τ_p): loss
  ∝ 1/(1+P/P_A). Slow SA (τ_p ≪ τ_A): loss ∝ exp(−U/U_A). Haus master
  equation: (1/ω_c²)d²a/dt² + [g(t)−ℓ(t)−ℓ₀]a − δT da/dt = 0. KLM: Kerr
  lens + hard aperture → effective fast SA ∝ n₂I. SESAM: ΔR modulation depth,
  F_sat saturation fluence, τ_A recovery. Soliton ML: anomalous GDD + SPM
  balance → N=1 soliton within gain window.
trigger:
  - designing or analyzing passively mode-locked femtosecond oscillators
  - choosing between KLM, SESAM, NPE, or hybrid mode-locking
  - computing pulse width, energy, stability from Haus equation
reasoning_role: passive_mode_locking
parent: reasoning.uo.mode_locking_active
retrieval_cost: 1
sign_convention: >
  τ_p = FWHM of |a(t)|². SA recovery time τ_A: fast if τ_A ≪ τ_p,
  slow if τ_p ≪ τ_A. SESAM: ΔR = maximum reflectivity change,
  F_sat = saturation fluence (μJ/cm²), τ_A = recovery time (ps to ns).
  KLM: n₂ > 0 for self-focusing. Soliton order N² = γ P₀ T₀² / |β₂| where
  T₀ = τ_p/1.763 (1/e intensity half-width for sech²). N=1 fundamental
  soliton: E_p = 2|β₂|/(γ T₀) ≈ 3.53|β₂|/(γ τ_p).
references:
  - ultrafast-optics: reasoning.uo.mode_locking_active (parent — ML concepts)
  - ultrafast-optics: reasoning.uo.pulse_propagation_linear (GDD → broadening)
  - ultrafast-optics: reasoning.uo.pulse_propagation_nlse_higher_order (soliton physics)
  - optics: reasoning.optics.laser_rate_equations (gain dynamics)
  - optics: reasoning.optics.gaussian_beam_optics (KLM spatial mode)
---

# reasoning.uo.mode_locking_passive — Saturable Absorber + Soliton → fs Pulses

## Core Picture

Passive mode-locking uses intensity-dependent loss to automatically favor
pulsed over CW operation: the peak of a short pulse saturates the absorber
(lower loss) while the wings see unsaturated (high) loss. Combined with
gain dynamics and dispersion, this produces femtosecond pulses without any
external modulator. The Haus master equation provides the unified framework,
with four major implementations: slow saturable absorber (dye), fast saturable
absorber (SESAM), artificial fast absorber (KLM, NPE), and soliton mode-locking
(Weiner §2, §6-7; Siegman §27.5-27.8; Diels-Rudolph §4-6).

## Derivation Sketch

### 1. Haus master equation (Weiner §2.3, eq 2.38; Haus 1975)

Assume small per-pass changes. After one round-trip, the pulse must reproduce
itself to within a time shift δT (typically ≪ τ_p):
```
(1/ω_c²) d²a/dt² + [g(t) − ℓ(t) − ℓ₀] a(t) − δT da/dt = 0       (2.38)
```
| Term | Physical meaning |
|------|-----------------|
| (1/ω_c²) d²a/dt² | Pulse broadening from finite gain bandwidth ω_c |
| g(t) a(t) | Time-dependent gain (saturable) |
| ℓ(t) a(t) | Time-dependent saturable loss |
| ℓ₀ a(t) | Fixed cavity loss |
| −δT da/dt | Time shift from asymmetric net gain window |

The d²/dt² term (broadening) must be balanced by ℓ(t)+g(t) terms (shortening).
This balance determines the steady-state pulse.

### 2. Saturable absorber classification (Weiner eq 2.42-2.45)

**Four-level SA model** (dye, semiconductor):
```
∂N₁/∂t = (N_A − N₁)/τ_A − (|a(t)|² N₁)/(P_A τ_A)       (2.40a)
P_A = ℏω₀ A_A/(σ_A τ_A)           [saturation power]
U_A = P_A τ_A                      [saturation energy]
```
Two limiting regimes:

**Fast SA** (τ_A ≪ τ_p, e.g., KLM, NPE):
```
N₁(t) = N_A / (1 + |a(t)|²/P_A)      (instantaneous, eq 2.42)
ℓ(t) ∝ N₁(t) ∝ 1/(1 + P/P_A)
```
Loss responds instantaneously to power → saturates at pulse PEAK.
The absorption follows the instantaneous intensity.

**Slow SA** (τ_p ≪ τ_A, e.g., semiconductor SESAM):
```
N₁(t) = N₁^(i) exp[−U(t)/U_A]       (cumulative energy, eq 2.44)
```
Loss depends on integrated pulse ENERGY, not instantaneous power.
The absorber saturates progressively during the pulse.

### 3. SESAM — semiconductor saturable absorber mirror (Keller 1992)

**Structure**: Bragg mirror + semiconductor absorber layer on top. Key parameters:

| Parameter | Symbol | Typical Range | Meaning |
|-----------|--------|--------------|---------|
| Modulation depth | ΔR | 0.5-3% | Maximum reflectivity change |
| Saturation fluence | F_sat | 10-100 μJ/cm² | Fluence to reduce absorption by 1/e |
| Recovery time | τ_A | 500 fs–100 ps (fast), 1-100 ns (slow) | Defect-mediated recombination |
| Non-saturable loss | ΔR_ns | 0.1-0.5% | Residual loss at full saturation |
| Damage threshold | F_dam | 1-10 mJ/cm² | Multi-photon absorption limit |

**Reflectivity vs fluence**:
```
R(F) = 1 − ΔR_ns − ΔR · exp(−F/F_sat)
```

**SESAM design rule**: For stable CW mode-locking without Q-switching:
```
|dR/dF| · E_p > T_R / τ_L    (Kärtner criterion)
```
where E_p is the intracavity pulse energy and τ_L is the upper-state lifetime.

### 4. Kerr Lens Mode-Locking (KLM) — artificial fast SA (Spence 1991)

**Physical mechanism**: The Kerr effect n = n₀ + n₂I produces self-focusing
of the intense pulse peak. With an intracavity hard aperture (slit), the
focused beam experiences lower diffraction loss → the peak sees lower loss
than the wings. This creates an effective ultrafast saturable absorber with
"recovery time" ∼ instantaneous (fs).

**KLM strength** (nonlinear ABCD matrix analysis):
The effective loss modulation depends on the nonlinear phase shift per pass:
```
ΔΦ_NL = (2π/λ) n₂ I_peak L_crystal
```
KLM typically requires ΔΦ_NL ∼ 0.1-0.5 rad. For Ti:sapphire (n₂ ≈ 3×10⁻¹⁶ cm²/W,
I_peak ∼ 10⁹ W/cm², L ≈ 3 mm): ΔΦ_NL ≈ 0.3 rad → sufficient for self-starting.

**Soft vs hard aperture KLM**:
- **Hard aperture**: Physical slit or pump beam as spatial filter. Stronger
  modulation, easier to design.
- **Soft aperture**: Overlap between cavity mode and pump beam changes with
  self-focusing. No additional optics needed.

**Cavity design** (astigmatically compensated Z-fold): Two curved mirrors
focus into the crystal at Brewster angle. One arm length adjusted to operate
near the edge of the stability zone → maximum KLM strength.

**Self-starting**: KLM is NOT typically self-starting — needs a perturbation
(transient spike from relaxation oscillations, or a slow SESAM to initiate).
Once started, KLM sustains 5-10 fs pulses from Ti:sapphire oscillators.

### 5. Nonlinear Polarization Rotation (NPE) — fiber artificial SA

In a fiber with polarization-dependent components (waveplates + polarizer),
the intensity-dependent polarization rotation (Kerr-induced birefringence)
converts amplitude modulation to polarization modulation. A polarizer then
converts this into intensity-dependent loss → effective fast SA.

**Transmission function** (sinusoidal):
```
T(I) ∝ sin²(ΔΦ_NL(I) + φ_bias)
ΔΦ_NL = (2π/λ) (n₂/3) I L_fiber   (for non-PM fiber)
```
Bias waveplates set the operating point. NPE is self-starting and widely
used in fiber oscillators.

### 6. Soliton mode-locking (Weiner §7)

When net cavity GDD is anomalous (β₂,net < 0), the pulse forms a soliton:
SPM balances GVD → sech² shape. The soliton order is:
```
N² = γ P₀ T₀² / |β₂,net|     where T₀ = τ_p/1.763 (sech²)
```
For stable mode-locking: N ≈ 1 (fundamental soliton). The soliton
energy-duration relation for N=1: E_p = 2|β₂|/(γ T₀) ≈ 3.53|β₂|/(γ τ_p).

**Soliton mode-locking with slow SA** (Weiner §7.2): The slow saturable
absorber opens a net gain window. Within this window, the pulse forms a
fundamental (N=1) soliton via the balance of anomalous GDD and SPM.
Pulse duration limited by gain bandwidth and soliton stability.

**Stretched-pulse (dispersion-managed) ML**: Alternating sections of normal
and anomalous dispersion. The pulse breathes (stretches and compresses) each
round-trip → lower peak power → reduced nonlinear phase → higher energy
pulses. Energy scaling: E_p ∝ √(β₂,pos − β₂,neg) vs soliton limit E_p ∝ 1/τ_p.

## Algorithm — Given Cavity Design → ML Operating Point

```
1. CHARACTERIZE cavity elements:
   - Gain: g₀, E_sat,g, Δν_g (FWHM bandwidth)
   - SA parameters: ΔR (or Δℓ₀), F_sat, τ_A
   - Dispersion: GDD_net per round-trip (from R14)
   - Kerr nonlinearity: γ = ω₀ n₂/(c A_eff) per pass
   - Loss: ℓ₀ linear cavity loss

2. DETERMINE ML REGIME:
   If τ_A < τ_p expected → fast SA (KLM, NPE).
   If τ_A > τ_p → slow SA (SESAM, dye).
   If β₂,net < 0 → soliton ML regime.
   If β₂,net alternates sign → stretched-pulse ML.

3. HAUS EQUATION ANALYSIS (fast SA approximation):
   ℓ(t) = ℓ₀ − κ|a(t)|² (for small saturation, KLM/NPE)
   → steady-state: sech² pulse, τ_p ≈ 4/(ω_c² κ E_p) — linear in inverse
   pulse energy (from balancing d²/dt² filter broadening ∝ 1/(ω_c²τ²)
   against SA shortening ∝ κE_p/(2τ)).

   For slow SA: ℓ(t) = ℓ₀ exp(−U(t)/U_A).
   → asymmetric pulse shape (steeper leading edge).

4. SOLITON ML (anomalous GDD):
   T₀² = |β₂,net|/(γ P₀) → E_p = 2P₀T₀ = 2|β₂,net|/(γ T₀)
   τ_p ≈ 3.53|β₂,net|/(γ E_p)   (fundamental soliton, N=1, sech²)
   E_p is determined by gain saturation: E_p ≈ E_sat,g · ln(g₀/ℓ₀).

5. CHECK STABILITY:
   - CW-ML: Q-switching suppressed if |dR/dF|·E_p > T_R/τ_L.
   - Multiple pulsing: if E_p exceeds 2× soliton energy → N=2 soliton
     or pulse splitting.
   - Harmonic ML: can be stable or chaotic.

6. OUTPUT: τ_p, E_p, P_peak = 0.88 E_p/τ_p, P_avg = E_p f_rep.
```

## Mode-Locking Technique Comparison

| Technique | SA type | τ_p range | Self-starting | Energy | Typical laser |
|-----------|---------|-----------|--------------|--------|-------------|
| KLM (Ti:sapphire) | Artificial fast | 5-100 fs | Usually not | 1-10 nJ | Ti:sapphire oscillator |
| SESAM (solid-state) | Semiconductor slow | 50 fs–10 ps | Yes | 10-100 nJ | Yb:YAG, Er:fiber |
| NPE (fiber) | Artificial fast | 50 fs–1 ps | Yes | 0.1-5 nJ | Er/Yb fiber |
| SESAM + soliton (fiber) | Slow + soliton | 100 fs–1 ps | Yes | 0.1-1 nJ | Er fiber |
| Stretched-pulse (fiber) | NPE + dispersion map | 30-100 fs | Yes | 1-10 nJ | Er/Yb fiber |
| SESAM + KLM hybrid | Semiconductor + Kerr | <10 fs | Yes | 1-5 nJ | Ti:sapphire |

## Edge Cases

- **Q-switched mode-locking (QML)**: When the saturable absorber is not
  strong enough, relaxation oscillations (Q-switching) modulate the pulse
  train envelope. Q-switching instability occurs when |dR/dF|·E_p < T_R/τ_L.
  Distinguished from CW-ML by periodic bursts of mode-locked pulses under
  a Q-switched envelope. Suppress by increasing SA modulation depth ΔR,
  reducing cavity losses, or increasing pump power (Kärtner criterion).
- **Multiple pulsing**: At high pump, gain supports >1 soliton. Splits into
  N=2,3... bound or separated solitons per round-trip.
- **CW breakthrough (CW-ML with CW background)**: Incomplete SA saturation
  leaves CW component coexisting with ML pulse. Increase SA modulation
  depth or use a slow SA + soliton effect to suppress.
- **Thermal lensing in KLM**: High average power heats crystal, changing
  cavity stability. Requires active or cryogenic cooling for >1 W output.

## Cross-References

- Weiner §2.3-2.4, §6-7; Siegman §27.5-27.8; Diels-Rudolph §4, §6
- Haus 1975 (master equation), Keller 1992 (SESAM), Spence 1991 (KLM)
- optics: reasoning.optics.laser_rate_equations (gain dynamics)
- optics: reasoning.optics.gaussian_beam_optics (KLM spatial mode analysis)
- ultrafast-optics: reasoning.uo.dispersion_compensation (GDD management)
- ultrafast-optics: reasoning.uo.pulse_propagation_nlse_higher_order (soliton N²)
- ultrafast-optics: knowledge.uo.mode_locked_laser_designs (practical cavity designs)
