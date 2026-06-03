---
skill_id: reasoning.optics.laser_rate_equations
type: reasoning
summary_50t: >
  dN₂/dt = R_p − N₂/τ − σ(N₂−N₁)I/hν. Threshold N_th, gain g=g₀/(1+I/I_sat).
  Steady-state: P_out = η(P_pump−P_th). Q-switch: store energy→dump→giant pulse.
  Mode locking: φ_n−φ_{n−1}=const → τ_p∼1/Δν. CPA: stretch→amplify→compress.
trigger:
  - designing laser oscillator/amplifier, computing output power
  - Q-switched or mode-locked pulse generation
reasoning_role: laser_dynamics
parent: reasoning.equilibrium_as_extremum
retrieval_cost: 1
sign_convention: >
  Population inversion ΔN = N₂ − N₁ (positive for gain). Pump rate R_p (atoms/s),
  stimulated emission rate = σcΔNφ/η. σ = stimulated emission cross-section (cm²).
  φ = intracavity photon density (photons/cm³). τ = upper-state lifetime.
  τ_c = cold cavity photon lifetime = 2L/[c(T+αL)]. Positive-going: dΔN/dt > 0
  means pumping faster than decay.
references:
  - landau-graph: reasoning.equilibrium_as_extremum (steady-state = pump-loss balance)
---

# reasoning.optics.laser_rate_equations — Pump → Gain → Coherent Output

## Core Picture

A laser is an optical oscillator: gain medium provides amplification, cavity
provides feedback. The dynamics are captured by coupled rate equations for
the population inversion ΔN = N₂−N₁ and the intracavity photon density φ
(Siegman §6-7, §12-13; Svelto §7-8).

## Derivation Sketch

Starting from `landau-graph: reasoning.equilibrium_as_extremum` (dynamic
systems approach a steady-state balance point where driving forces and
losses are equal):

1. **Rate equations as coupled dynamical system**: The laser is a driven
   dissipative system. Pumping drives ΔN away from thermal equilibrium;
   stimulated emission and spontaneous decay bring it back. The minimal
   model couples two reservoirs: inversion ΔN and photon number φ:
   ```
   dΔN/dt = R_p − ΔN/τ − (σc/η) ΔN φ
   dφ/dt   = (σc/η) ΔN φ − φ/τ_c + β ΔN/τ
   ```
   The product ΔN·φ is the non-negotiable coupling: photons are created
   by stimulated emission (∝ σ ΔN φ) and lost via cavity decay (∝ φ/τ_c).

2. **Steady-state = equilibrium as extremum** (consuming parent edge):
   Setting d/dt = 0 yields two regimes. Below threshold (φ→0): ΔN_ss = R_p τ
   (inversion grows linearly with pump). Above threshold: ΔN = ΔN_th
   (CLAMPED — inversion saturates, cannot exceed threshold regardless of
   pump). The clamping is the physical manifestation of "equilibrium as
   extremum": the system finds the balance point where gain = loss, and
   excess pump converts directly to output photons. This is a bifurcation
   at P_pump = P_th — the system switches from amplifier to oscillator.

3. **Einstein A and B coefficients → σ** (connecting quantum to macroscopic):
   The stimulated emission cross-section derives from the atomic dipole
   moment via (Siegman §2-3, Svelto §2):
   ```
   σ(ν) = (λ²/8π) A₂₁ g(ν)   where A₂₁ = Einstein A coefficient,
                                      g(ν) = normalized lineshape.
   ```
   For a Lorentzian line (homogeneous, width Δν): σ_peak = λ²/(4π² Δν τ_sp).
   For Gaussian (inhomogeneous, width Δν_D): σ_peak = λ²√(ln 2)/(4π τ_sp Δν_D).
   This bridges the parent's macroscopic equilibrium to the atomic
   dipole matrix element: σ ∝ |μ₁₂|² (Fermi's golden rule).

## Algorithm

```
1. RATE EQUATIONS (4-level laser, homogeneously broadened):
   dΔN/dt = R_p − ΔN/τ − (σ c/η) ΔN φ
   dφ/dt   = (σ c/η) ΔN φ − φ/τ_c + β ΔN/τ
   where: R_p = pump rate, τ = upper-state lifetime, σ = stimulated
   emission cross-section, τ_c = cold cavity photon lifetime.

2. THRESHOLD: steady-state d/dt=0, φ→0.
   ΔN_th = η/(σ c τ_c). R_p,th = ΔN_th/τ.
   Threshold pump power: P_th = hν_p R_p,th V_mode.

3. STEADY-STATE ABOVE THRESHOLD:
   ΔN = ΔN_th (clamped at threshold).
   φ = (τ_c/hν)[P_pump − P_th].
   Output: P_out = T φ hν A_beam = η_slope (P_pump − P_th).

4. GAIN SATURATION (Siegman §7):
   g(I) = g₀ / (1 + I/I_sat).
   I_sat = hν/(σ τ) for 4-level systems.

5. RELAXATION OSCILLATIONS: small perturbation around steady-state →
   damped oscillation at ω_rel ≈ √[(σc/η)φ/τ] ∼ 10⁵−10⁶ rad/s.
```

## Beyond the Ideal 4-Level Model

**Quasi-3-level systems** (Yb:YAG, Er:glass, Er:fiber — Svelto §7):
Lower laser level is a STARK SUBLEVEL of the ground manifold with
thermal population N₁ = f₁ N_total exp(−ΔE₁/kT). Unlike ideal 4-level
(N₁=0 always), quasi-3-level lasers must overcome GROUND-STATE
ABSORPTION (GSA). Modified threshold:
```
ΔN_th = N_total (f₂ + f₁) / (σ_e + σ_a) · [σ_a + α_cavity/N_total]
```
where f₁, f₂ = Boltzmann factors, σ_a, σ_e = absorption/emission cross-sections
at the laser wavelength. The transparency inversion is N_tr = f₁ N_total
— pump must reach transparency before any net gain exists. This raises
threshold significantly (Yb:YAG at 300K: η_overall ~ 20% below 200 W pump,
improves with cryogenic cooling where f₁ → 0). Key design parameters:
pump intensity must exceed I_min = hν_p/(σ_p τ) · (σ_a/σ_e) for transparency.

**Spatial hole burning** (Siegman §12.4): In standing-wave cavities, the
intracavity intensity forms a sinusoidal pattern ∝ sin²(2πnz/λ). Population
inversion is depleted ONLY at the antinodes, leaving undepleted inversion at
the nodes. This allows other longitudinal modes to reach threshold at these
spatial positions → MULTI-MODE operation even in homogeneously broadened
media. Mitigation: ring cavity (traveling wave, no standing wave), twisted-mode
cavity (circular polarization eliminates intensity modulation), or unidirectional
ring with optical diode.

**Inhomogeneous broadening** (gas lasers, solid-state at low temperature,
semiconductor quantum dots): Different atoms/ions have different resonant
frequencies within the gain bandwidth. The gain saturates as a Gaussian
"hole" at the lasing frequency (spectral hole burning), not uniformly across
the whole lineshape. Multi-mode oscillation is natural — each mode burns its
own hole. For a Gaussian lineshape of width Δν_D, the saturated gain for
mode i is g_i = g₀ exp[−4ln2(ν_i−ν₀)²/Δν_D²] / (1 + I_i/I_sat).
The number of oscillating modes is determined by how many hole-burned
frequencies still exceed threshold.

**Thermal lensing** (Siegman §19): Pump-induced heating creates a radial
temperature gradient dT/dr < 0 → dn/dT changes refractive index → effective
positive lens (for most solid-state media with dn/dT > 0). Focal length:
```
f_th ∝ (κ A_pump) / (P_heat dn/dT)
```
where κ = thermal conductivity, P_heat = (1−η)P_pump. Thermal lensing changes
resonator stability → power-dependent mode size → can cause Q-switching
instability or even cavity failure. Mitigation: athermal design (composite
crystal with undoped endcaps as heat spreaders), cryogenic operation
(dn/dT decreases dramatically), or negative-branch unstable resonator
designs that are less sensitive to thermal lens power.

**Schawlow-Townes linewidth** (fundamental quantum limit — Svelto §7.8):
The finite photon lifetime and spontaneous emission set a fundamental
linewidth for a CW laser:
```
Δν_ST = (π hν (Δν_c)²) / P_out   where Δν_c = 1/(2πτ_c) = cavity linewidth
```
For typical solid-state lasers: Δν_ST ~ 10⁻³−10⁻¹ Hz (far below technical
noise). Modified for semiconductor lasers (linewidth enhancement factor α_H,
Henry 1982): Δν = Δν_ST · (1 + α_H²), where α_H = (dn'/dN)/(dn''/dN) is the
ratio of carrier-induced index change to gain change. α_H ~ 3-7 in bulk
semiconductors → linewidth enhanced by 10-50×.

## Q-Switching (Siegman §24, Svelto §8)

```
1. Hold cavity at low Q (shutter closed) → pump stores energy in gain medium.
2. Suddenly switch to high Q → φ builds from noise → ΔN depleted.
3. Giant pulse: P_peak ≈ (hν/τ_c) ΔN_i V, τ_pulse ∼ τ_c.
   Energy: E_out ≈ (ΔN_i−ΔN_f) hν V ≈ η_ext E_stored.
```

## Mode Locking (Siegman §27, Svelto §8)

N longitudinal modes with fixed phase relation φ_n−φ_{n−1} = const → periodic
pulse train. τ_p ≈ 1/Δν (transform limit). f_rep = c/2L.
Active: AM/FM modulator at f_rep. Passive: saturable absorber (fast: SESAM, slow: dye).
KLM: Kerr lens from n₂(I) → self-focusing → higher gain for pulsed mode.

## CPA (Chirped Pulse Amplification, Nobel 2018)

Stretch (τ→ns) → amplify (avoid damage) → compress (τ→fs). Grating pair
provides positive/negative GDD. P_peak increased by 10³−10⁵×.

## Edge Cases

- **CW threshold vs. pulsed threshold**: Q-switched or mode-locked lasers may
  have different effective thresholds due to time-dependent dynamics. For
  Q-switching: pump duration must exceed τ for efficient energy storage
  (~3τ for 95% of steady-state). If pump pulse < τ, switch to time-dependent
  rate equation solution (numerical integration) rather than steady-state formulas.
- **ASE (Amplified Spontaneous Emission)**: In high-gain amplifiers, spontaneous
  emission is amplified along the gain path, depleting stored energy before
  the signal pulse arrives. Critical in fiber amplifiers and disk lasers.
  ASE fraction grows as ∝ G (gain) — limits single-pass gain to ~30-40 dB.
  Mitigation: multi-pass or regenerative amplification, or use ASE-suppressing
  index-guiding.
- **Gain narrowing in CPA**: The finite gain bandwidth |g(ν)| means spectral
  wings are amplified less than the peak. After N passes through gain medium,
  the effective bandwidth shrinks as Δν_eff ≈ Δν_gain / √(ln G). For high
  gain (G > 10³), this can limit pulse duration to τ_p > 1/Δν_eff even if
  the seed bandwidth is larger. Mitigation: regenerative pulse shaping
  (intracavity spectral filter that counteracts gain narrowing), or
  OPCPA (optical parametric CPA — parametric gain can be broader).
- **Thermal lensing instability**: When f_th becomes comparable to cavity
  mirror radii, the resonator enters unstable regime. Monitor output power
  rollover (not just saturation) — if P_out drops while P_pump increases,
  thermal lensing has destabilized the cavity. Remedy: redesign cavity
  for lower sensitivity to internal lens (use shorter cavity, larger
  fundamental mode, or convex mirrors for compensation).

## Cross-References

- Siegman §6-7, §12-13, §24, §27; Svelto §7-8
- landau-graph: reasoning.equilibrium_as_extremum (steady-state balance;
  Derivation Sketch step 2 explicitly consumes this parent: laser threshold
  is a bifurcation to oscillation — the extremum principle determines the
  stable operating point)
- landau-graph: reasoning.normal_mode_decomposition (N cavity modes)
- optics: reasoning.optics.ultrashort_pulse_generation (mode locking: the
  rate equations + fixed phase → pulse train. Bidirectional: this node
  provides the gain dynamics needed for mode-locking analysis)
