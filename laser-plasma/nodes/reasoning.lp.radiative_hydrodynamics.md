---
skill_id: reasoning.lp.radiative_hydrodynamics
type: reasoning
summary_50t: >
  Radiative hydrodynamics: radiation transport coupled to fluid motion.
  Radiation transfer equation in diffusion limit: F_rad = −(16σ T³/3κ_R)∇T.
  Rosseland mean opacity κ_R, Marshak wave (radiation heat front): x_f(t)
  ∝ t^{1/2}. Radiation pressure P_rad = aT⁴/3. Flux-limited diffusion for
  optically thin regions. Applications: ICF hohlraum, stellar interiors,
  radiative shock structure.
trigger:
  - computing radiation heat wave propagation speed
  - analyzing radiation-hydro coupling in ICF capsule implosions
  - modeling radiation preheat effects on shock structure
reasoning_role: radiative_hydrodynamics
parent: reasoning.lp.shock_waves_plasma
retrieval_cost: 1
sign_convention: >
  a = radiation constant = 7.56×10⁻¹⁵ erg/cm³/eV⁴.
  σ = ac/4 = Stefan-Boltzmann. κ_R = Rosseland mean opacity (cm²/g).
  Optical depth τ = ∫κρ dx. Diffusion valid for τ ≫ 1.
---

# reasoning.lp.radiative_hydrodynamics — Radiation-Fluid Coupling

## Core Picture

At temperatures T > 100 eV, radiation energy density (U_rad = aT⁴) and
pressure (P_rad = aT⁴/3) become comparable to or exceed the material
energy/pressure. The radiation field transports energy non-locally,
creating radiative heat fronts (Marshak waves) and modifying shock
structure. Radiative hydrodynamics couples the radiation transfer equation
to the fluid equations — essential for ICF hohlraum physics, astrophysical
flows, and high-Z plasma dynamics under intense laser irradiation
(Zel'dovich & Raizer §10, Drake §6-8, Mihalas & Mihalas).

## Derivation Sketch

### 1. Radiation-hydrodynamic equations

The coupled system:
```
∂ρ/∂t + ∇·(ρv) = 0                                     [mass]
ρ(∂v/∂t + v·∇v) = −∇(p + P_rad)                        [momentum]
ρ(∂ε/∂t + v·∇ε) = −p∇·v − ∇·F_rad + S_laser           [energy]
```

The radiation field adds:
- P_rad = aT⁴/3 (isotropic radiation pressure, valid at τ ≫ 1)
- F_rad = radiation energy flux
- −∇·F_rad = net radiation heating/cooling

The radiation-material coupling term (emission and absorption) in the
energy equation couples the material temperature T_m and radiation
temperature T_r.

### 2. Diffusion approximation (optically thick)

For τ ≫ 1 (many mean free paths), radiation transport reduces to diffusion:
```
F_rad = −(16 σ T³ / 3 κ_R ρ) ∇T    [radiative diffusion]
```
where κ_R is the Rosseland mean opacity (frequency-averaged, inversely
weighted by ∂B_ν/∂T):
```
κ_R⁻¹ = ∫ κ_ν⁻¹ (∂B_ν/∂T) dν / ∫ (∂B_ν/∂T) dν
```

The radiative thermal conductivity: K_rad = 16σT³/3κ_Rρ.

### 3. Marshak wave — radiative heat front

For a constant-temperature boundary at x=0, the heat front propagates
into cold material:
```
∂(aT⁴)/∂t = ∂/∂x (16σT³/3κ_Rρ ∂T/∂x)
```

Self-similar solution (Marshak 1958):
```
x_f(t) = √(K_rad t / aT₀³) ≈ √(16σT₀ t / 3κ_R ρ a)
       ∝ t^{1/2} (diffusive scaling)
```

Front velocity: v_f ≈ x_f/2t ∝ t^{-1/2} (decelerating).
For T₀ = 300 eV in Au plasma at ρ = 1 g/cm³: v_f ~ 10⁷ cm/s, x_f ~ 1 mm
in 10 ns.

### 4. Flux-limited diffusion

In optically thin regions (τ < 1), the diffusion approximation fails
(F → ∞ as κ→0). The flux limiter caps F at the free-streaming value:
```
F_max = f c aT⁴    [free-streaming limit]
F_rad = min(F_diffusion, f c aT⁴)
```
where f ≈ 0.1–0.3 is the flux limiter. Standard in ICF codes.

### 5. Radiation-modified shock structure

When a shock propagates into a medium, radiation from the shocked region
preheats the upstream material:

- **Subcritical shock** (v_shock < v_crit): the radiative precursor is
  optically thin. Upstream preheat modifies initial conditions but
  shock remains discontinuous.

- **Supercritical shock** (v_shock > v_crit): the precursor becomes
  optically thick. The shock broadens into a continuous transition
  (no true discontinuity). T_preheat ≈ T_post before shock arrival.

- **Critical velocity**: v_crit depends on opacity and temperature.
  For air at STP: v_crit ≈ 80 km/s. For Au plasma: v_crit ≈ 200 km/s.

### 6. Cooling regimes and opacity scaling

**Bremsstrahlung cooling** (low-Z, high T):
```
j_ff ∝ n_e n_i Z² √T    [volume emissivity]
```
**Line radiation** (moderate T): dominant at T ~ 100–1000 eV for mid-Z
materials. Complex → opacity tables required.

**Rosseland opacity scaling** (approximate):
```
κ_R ∝ Z ρ T^{−3.5}    [Kramers' law for free-free, T > Z² Ry]
```
High-Z → high opacity → lower radiative conductivity → slower Marshak wave.

## Algorithm — Given (T₀, ρ, Z) → Heat Wave Propagation

```
1. ESTIMATE κ_R from material and T:
   κ_R ≈ C Z ρ T^{-3.5} (Kramers, free-free)
   For T < 500 eV: include bound-free and line contributions.

2. COMPUTE radiative conductivity: K_rad = 16σT³/3κ_Rρ.

3. MARSHAK FRONT: x_f(t) = √(4 K_rad t / aT³).

4. CHECK optical depth: τ(x) = ∫₀ˣ κ_R ρ dx.
   If τ < 1: use flux-limited diffusion or full transport.

5. RADIATION PRESSURE: P_rad/P_material = aT⁴/3nk_B T.
   Important when P_rad > P_material → T > (3nk_B/a)^{1/3}.
```

## Edge Cases

- **High-Z vs low-Z**: Au (Z=79) has much higher opacity than CH (Z~3.5)
  → Au hohlraum walls contain radiation, CH capsules are more transparent.
- **Non-LTE**: at low density and high temperature, the populations deviate
  from Saha-Boltzmann → full non-LTE atomic kinetics needed.
- **Two-temperature models**: for low collisional coupling between electrons
  and ions (T_e ≠ T_i), separate energy equations required.

## Cross-References

- Zel'dovich & Raizer §10, Drake §6-8
- Marshak, Phys. Fluids 1, 24 (1958) — original Marshak wave
- Mihalas & Mihalas, *Foundations of Radiation Hydrodynamics* (1984)
- laser-plasma: reasoning.lp.shock_waves_plasma (parent — shock context)
- laser-plasma: reasoning.lp.hohlraum_physics (radiative transport in hohlraum)
- laser-plasma: reasoning.lp.fast_ignition (electron vs radiation transport)
