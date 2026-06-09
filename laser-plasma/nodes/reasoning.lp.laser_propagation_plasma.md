---
skill_id: reasoning.lp.laser_propagation_plasma
type: reasoning
summary_50t: >
  Laser propagation in plasma: EM dispersion ω² = ω_p² + c²k².
  Critical density n_c = ε₀ m_e ω²/e² = 1.1×10²¹/λ²(μm) cm⁻³.
  Below n_c: propagating (v_ph > c, v_g = c²/v_ph). Above n_c: evanescent
  (skin depth c/ω_p). Oblique incidence: s-/p-polarization, turning point
  at n_e = n_c cos²θ. Relativistic: n_c → γn_c (induced transparency at a₀>1).
  Inverse bremsstrahlung absorption → collisional damping.
trigger:
  - computing where laser light reflects in a plasma density profile
  - understanding relativistic transparency threshold
  - designing density profiles for laser-plasma experiments
reasoning_role: laser_plasma_propagation
parent: reasoning.plasma.dielectric_tensor_magnetized
retrieval_cost: 1
sign_convention: >
  Time convention e^{−iωt}. EM wave: E = E₀ e^{i(kz−ωt)}.
  Plasma frequency ω_p = √(n_e e²/ε₀ m_e). Critical density n_c(λ).
  Scattering parameter: incident angle θ from normal. s-pol = E ⟂ plane
  of incidence. p-pol = E in plane of incidence.
---

# reasoning.lp.laser_propagation_plasma — ω² = ω_p² + c²k² → n_c

## Core Picture

An electromagnetic wave in an unmagnetized plasma obeys the dispersion
relation ω² = ω_p² + c²k². When ω > ω_p the wave propagates with phase
velocity v_ph = c/√(1−ω_p²/ω²) > c and group velocity v_g = c√(1−ω_p²/ω²) < c.
At the critical density where ω_p = ω, the wavevector k→0 and the wave
reflects. The critical density is the fundamental length scale of
laser-plasma interaction (Kruer §1, Gibbon §3, Macchi §3).

## Derivation Sketch

### 1. EM wave in cold unmagnetized plasma

From the fluid equations for electrons (ions stationary):
```
m_e ∂v/∂t = −e E
∂n_e/∂t + n₀ ∇·v = 0
∇×E = −∂B/∂t,   ∇×B = μ₀(−e n₀ v) + (1/c²)∂E/∂t
```
Combining yields the wave equation:
```
(∂²/∂t² − c²∇² + ω_p²) E = 0
```
For a plane wave E ∝ e^{i(k·r−ωt)}:
```
ω² = ω_p² + c²k²         (EM dispersion in plasma)
```

### 2. Critical density

Setting k → 0 (wave reflection):
```
ω² = ω_p² → n_c = ε₀ m_e ω²/e²
```
In practical units:
```
n_c[cm⁻³] = 1.1 × 10²¹ / λ²[μm]
```
| Laser | λ (μm) | n_c (cm⁻³) |
|-------|--------|-----------|
| Nd:glass | 1.054 | 1.0 × 10²¹ |
| Ti:sapphire | 0.8 | 1.7 × 10²¹ |
| KrF | 0.248 | 1.8 × 10²² |
| CO₂ | 10.6 | 1.0 × 10¹⁹ |
| 4th harmonic Nd | 0.263 | 1.6 × 10²² |

### 3. Propagation below n_c

For n_e < n_c: real k, propagating wave.
```
v_ph = ω/k = c/√(1−n_e/n_c) > c
v_g = ∂ω/∂k = c√(1−n_e/n_c) < c
```
The refractive index N = ck/ω = √(1−n_e/n_c). As n_e → n_c, N → 0
→ wave slows, wavelength stretches, eventual reflection.

### 4. Evanescence above n_c

For n_e > n_c: k = iκ is imaginary → field decays as e^{−κz}:
```
κ = (ω_p/c) √(1 − ω²/ω_p²) ≈ ω_p/c   [for ω ≪ ω_p]
δ_skin = 1/κ ≈ c/ω_p
```
Skin depth: for n_e = 10n_c at 800 nm, δ_skin ≈ 50 nm.

### 5. Oblique incidence — turning point

With density gradient along z and oblique incidence angle θ:
- **s-polarization** (E ⟂ plane of incidence):
  k²(z) = (ω²/c²)(1 − n_e(z)/n_c) − k_y². Reflects at n_e = n_c cos²θ.
- **p-polarization** (E in plane of incidence):
  Electric field has component along ∇n_e → drives plasma oscillation
  → **resonance absorption** at n_e = n_c cos²θ (see R2).

The turning point is n_e = n_c cos²θ, not n_c. For 45° incidence:
reflection at n_e = 0.5 n_c.

### 6. Relativistic corrections — induced transparency

When the electron quiver velocity approaches c (a₀ = eE₀/m_eωc > 1),
the effective mass increases: m_e → γ m_e with γ = √(1+a₀²/2).
```
ω_p → ω_p/√γ,   n_c → γ n_c
```
An initially overdense plasma (n_e > n_c) can become transparent at
sufficiently high intensity (a₀ > 1). This is **relativistic induced
transparency** (see R10).

## Algorithm — Given Density Profile → Propagation

```
1. COMPUTE n_c for the laser wavelength.

2. DETERMINE propagation region:
   For linear density ramp n_e(z) = n_c · z/L_n:
   - Turning point z_t = L_n cos²θ for oblique incidence
   - Reflection at z = z_t

3. FOR s-polarization below turning point:
   E(z) ∝ sin(∫_z^{z_t} k(z') dz' + π/4)  [WKB solution]
   with k(z) = (ω/c) √(cos²θ − n_e(z)/n_c).

4. CHECK relativistic regime: a₀ > 1 → n_c → γ n_c.
   Induced transparency when γ > n_e/n_c.

5. WKB validity: (1/k²)(dk/dz) ≪ 1. Fails near turning point →
   use Airy function connection (swelling factor).
```

## Edge Cases

- **WKB breakdown near turning point**: k→0 → WKB diverges.
  Field swelling factor: |E|² at turning point ≈ 3.6 (ωL_n/c)^{2/3} |E_fs|².
- **Steep gradients** (L_n ∼ λ): geometrical optics fails → full wave
  solution (Helmholtz) needed.
- **Collisional damping**: ν_ei adds imaginary part to k → spatial decay
  (inverse bremsstrahlung absorption — see R2).
- **Magnetic fields**: External B₀ changes dispersion → R-wave/L-wave
  cutoffs (whistler regime). Cross-ref: `plasma.dielectric_tensor_magnetized`.

## Cross-References

- Kruer §1-2, Gibbon §3, Macchi §3
- plasma: reasoning.plasma.dielectric_tensor_magnetized (parent — general plasma dielectric)
- laser-plasma: reasoning.lp.laser_absorption_mechanisms (energy deposition)
- laser-plasma: reasoning.lp.relativistic_transparency (n_c → γn_c)
