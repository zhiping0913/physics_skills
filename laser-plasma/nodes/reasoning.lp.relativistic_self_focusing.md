---
skill_id: reasoning.lp.relativistic_self_focusing
type: reasoning
summary_50t: >
  Relativistic self-focusing: electron mass increase γ = √(1+a₀²/2)
  modifies refractive index N ≈ 1−ω_p²/(2γω²) → on-axis index higher →
  nonlinear lens. Critical power P_cr[GW] ≈ 17 (ω/ω_p)² = 17 n_c/n_e.
  P > P_cr → beam self-focuses. Coupled with ponderomotive channeling
  (density expulsion). Filamentation instability when spot size >
  plasma wavelength. Cross-domain: Kerr self-focusing analog.
trigger:
  - computing critical power for relativistic self-focusing
  - determining if a given laser will self-focus in plasma
  - understanding beam propagation stability in underdense plasma
reasoning_role: relativistic_self_focusing
parent: reasoning.lp.laser_propagation_plasma
retrieval_cost: 1
sign_convention: >
  P_cr = critical power for self-focusing. N = refractive index = ck/ω.
  γ ≈ √(1+a₀²/2) for CP, γ ≈ √(1+a₀²) for LP (approximate).
  Filamentation: perturbation growth rate Γ.
---

# reasoning.lp.relativistic_self_focusing — γ Modulation → Nonlinear Lens

## Core Picture

In underdense plasma, the relativistic mass increase of quivering electrons
(γ = √(1+a₀²/2)) reduces the local plasma frequency ω_p/√γ. This increases
the refractive index N = √(1−ω_p²/γω²) on the laser axis where intensity is
highest. The on-axis phase velocity is slower than off-axis → wavefront
curvature → focusing. When the laser power exceeds a critical power P_cr,
self-focusing overcomes diffraction and the beam collapses. This is the
relativistic analog of Kerr self-focusing in optical fibers (Sun et al. 1987,
Sprangle et al. 1987, Borisov et al. 1992).

## Derivation Sketch

### 1. Relativistic refractive index

Cold, unmagnetized plasma with relativistic electron motion:
```
ε = 1 − ω_p²/(γ ω²)
N = √ε ≈ 1 − ω_p²/(2γ ω²)    [underdense: ω_p ≪ ω]
```

where γ = √(1 + ⟨v²⟩/c²). For a laser field:
```
γ ≈ √(1 + a₀²/2)    [circular polarization, exact]
γ ≈ √(1 + a₀²)      [linear polarization, cycle-averaged approx]
```

For a Gaussian beam (peak a₀ on axis, a₀→0 at edge):
```
N(r) ≈ 1 − (ω_p²/2ω²) · 1/γ(r)
```

On-axis: γ large → N higher. Off-axis: γ→1 → N lower.
→ The plasma acts as a POSITIVE lens (focusing).

### 2. Critical power

Self-focusing overcomes diffraction when the focusing strength exceeds
the diffraction divergence. Balancing the nonlinear focusing angle
θ_NL ≈ √(ΔN) against the diffraction angle θ_diff ≈ λ/(πw₀):
```
P_cr[GW] = (4πε₀ m²c⁵/e²) · (ω²/ω_p²) = (2m_e²c⁵/e²) · (ω²/ω_p²)
         = 2 × (ω²/ω_p²) × 4.3 GW
         ≈ 17 (ω/ω_p)² GW
         = 17 (n_c/n_e) GW
```

For n_e = 10¹⁹ cm⁻³, λ₀ = 0.8 μm (n_c ≈ 1.7×10²¹): P_cr ≈ 2.9 TW.
For n_e = 10¹⁸ cm⁻³: P_cr ≈ 29 TW.

A 100 TW laser at n_e = 10¹⁹ cm⁻³ has P/P_cr ≈ 34 → strong self-focusing.

### 3. Self-focusing length

The characteristic length for self-focusing (for P ≫ P_cr):
```
Z_sf ≈ Z_R / √(P/P_cr − 1)
```
where Z_R = πw₀²/λ is the Rayleigh length.

For P = 10 P_cr: Z_sf ≈ Z_R/3. The beam self-focuses within a fraction
of its diffraction length.

### 4. Coupling with ponderomotive channeling

The ponderomotive force ALSO expels electrons from the axis (R3),
creating a density channel: n_e(r) < n_e0. This reduces ω_p locally
→ further increases N on-axis → ADDITIONAL focusing.

Total focusing strength:
```
ΔN_total = ΔN_relativistic + ΔN_ponderomotive
         ≈ (ω_p²/4ω²)(a₀²) + (ω_p²/2ω²)(δn_e/n_e)
```

Both effects are of order a₀² ω_p²/ω² → similar magnitude.
At a₀ > 1, ponderomotive channeling can dominate.

### 5. Filamentation instability

A plane wave (or large beam with diameter ≫ λ_p) is unstable to
transverse modulations. Density/intensity perturbations grow:
```
Γ_max ≈ (ω_p²/8ω) a₀²    [growth rate, relativistic filamentation]
```
Most unstable scale: λ_⟂ ≈ λ_p (the plasma wavelength).

Consequences: smooth beam breaks into filaments of width ~λ_p.
Each filament carries ~P_cr power. Filamentation limits the maximum
useful beam diameter to ~few λ_p.

## Algorithm — Given (P, λ₀, n_e, w₀) → Focusing Behavior

```
1. COMPUTE P_cr = 17 (n_c/n_e) GW.
   P_cr[GW] = 17 × (1.1×10²¹/λ²[μm]) / n_e[cm⁻³]
             = 1.9×10²² / (n_e[cm⁻³] · λ²[μm])

2. COMPUTE P/P_cr. If > 1: self-focusing occurs.

3. SELF-FOCUSING LENGTH: Z_sf ≈ Z_R / √(P/P_cr − 1).

4. CHECK filamentation: if w₀ > λ_p, transverse modulation growth.
   Growth length: L_fil ≈ 1/Γ_max ≈ 8ω/(ω_p² a₀²).

5. MATCHED SPOT: for stable guiding, P ≈ P_cr and w₀ ≈ λ_p.
```

## Relativistic vs Kerr Self-Focusing

| Aspect | Relativistic Plasma | Kerr Medium (fiber) |
|--------|-------------------|---------------------|
| Nonlinearity | γ(r) mass increase | n₂ intensity |
| Δn | ∝ a₀² (saturates) | ∝ I (no saturation) |
| P_cr | 17 n_c/n_e GW | λ²/(2π n₀ n₂) |
| Saturation | a₀ ≫ 1 → γ saturates | None (until damage) |
| Accompanying | Ponderomotive channeling | Raman/Brillouin |
| Damage threshold | None | ~GW/cm² |

## Edge Cases

- **Saturation at a₀ ≫ 1**: γ grows with a₀ → the nonlinear index change
  ΔN ∝ 1−1/γ saturates. For a₀→∞, ΔN → ω_p²/2ω² (maximum).
  At extreme a₀, self-focusing saturates — beam cannot focus indefinitely.
- **Pulse length**: self-focusing requires τ_L > Z_sf/c (few × λ_p/c).
  Ultra-short pulses (τ_L < 100 fs at n_e=10¹⁹) may not self-focus.
- **Electron cavitation**: at extreme P/P_cr, electrons are fully expelled
  → hollow channel → beam guided, not focused further.

## Cross-References

- Sun et al., PF 30, 526 (1987); Sprangle et al., PRL 1987; Borisov et al. 1992
- Brabec §3-4, Gibbon §5, Macchi §6
- laser-plasma: reasoning.lp.laser_propagation_plasma (parent — N(r) from dispersion)
- laser-plasma: reasoning.lp.ponderomotive_force (coupled channeling effect)
- ultrafast-optics: reasoning.uo.pulse_propagation_nlse_higher_order (Kerr self-focusing analog)
