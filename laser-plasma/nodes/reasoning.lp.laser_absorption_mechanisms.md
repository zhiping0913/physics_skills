---
skill_id: reasoning.lp.laser_absorption_mechanisms
type: reasoning
summary_50t: >
  Four absorption regimes by Iλ²: collisional (inverse bremsstrahlung,
  α_IB ∝ n_e²T_e^{−3/2}/√(1−n_e/n_c)), resonance absorption (p-pol,
  obliquely incident, swelling field drives plasma wave), Brunel vacuum
  heating (steep gradient, v_osc ≫ v_th), j×B heating (relativistic,
  a₀>1, 2ω oscillation). Total absorption fraction f_A(Iλ²) transitions
  from collisional→resonance→Brunel→j×B with increasing intensity.
trigger:
  - computing laser energy deposition into plasma
  - determining dominant absorption mechanism for given I, λ, T_e
  - designing target for efficient laser coupling
reasoning_role: laser_absorption
parent: reasoning.lp.laser_propagation_plasma
retrieval_cost: 1
sign_convention: >
  Absorption fraction f_A = 1 − R (R = reflected fraction).
  Collision frequency ν_ei = (4√2π/3) n_e Z e⁴ lnΛ/(√m_e T_e^{3/2}).
  p-polarization = E in plane of incidence. Brunel: v_osc = eE₀/m_eω.
  j×B: oscillatory at 2ω, drives density perturbations.
---

# reasoning.lp.laser_absorption_mechanisms — Four Regimes by Iλ²

## Core Picture

Laser energy couples to plasma through four distinct mechanisms, each
dominant in a different (I, λ, T_e, L_n) regime. At low intensities
(Iλ² < 10¹⁴ W·μm²/cm²), collisional inverse bremsstrahlung dominates.
At intermediate, resonance absorption converts p-polarized light to
plasma waves near the critical surface. At high intensities, collisionless
mechanisms (Brunel vacuum heating, j×B heating) take over. The total
absorption fraction f_A(Iλ²) is the fundamental coupling efficiency in
laser-plasma interaction (Kruer §3-4, Gibbon §3-4).

## Derivation Sketch

### 1. Inverse bremsstrahlung (collisional absorption)

The electron-ion collision frequency damps the coherent electron quiver:
```
ν_ei = (4√2π/3) (n_e Z e⁴ lnΛ)/(√m_e T_e^{3/2})
```

Energy damping rate per unit volume: ⟨J·E⟩ = (ν_ei ω_p²/ω²) ε₀|E|²/2.

**Spatial damping rate** for a propagating wave:
```
κ_IB = (ν_ei/c) (ω_p²/ω²) / √(1−ω_p²/ω²)
```

**Absorption fraction** for linear density profile L_n:
```
f_A = 1 − exp(−(32/15) (ν_ei/c) L_n)
```
Dominant for Iλ² < 10¹⁴ W·μm²/cm² (collision frequency exceeds growth
rate of parametric instabilities). Scales as ∝ n_e Z/T_e^{3/2} λ².

### 2. Resonance absorption (p-polarized oblique incidence)

For p-polarized light incident at angle θ on a density gradient:
the electric field component along ∇n_e resonantly drives a plasma
oscillation at the turning point n_e = n_c cos²θ.

**Physics**: The p-polarized field tunnels from the turning point to
the critical surface (n_e = n_c) where its longitudinal component
drives a plasma wave:
```
∇·E = −(e/ε₀) δn_e → electrostatic field at ω = ω_p
```
The plasma wave damps collisionlessly (Landau damping) or collisionally,
depositing energy.

**Absorption fraction** (Ginzburg 1964, Denisov 1957):
```
f_A ≈ ½ φ²(τ)    where τ = (ωL_n/c)^{1/3} sin θ
```
φ(τ) ≈ 2.3 τ exp(−2τ³/3) for τ ≲ 1. Maximum f_A ≈ 0.5 at τ ≈ 0.8.
Dominant for 10¹⁴ < Iλ² < 10¹⁶ W·μm²/cm² (for long L_n).

### 3. Brunel vacuum heating (not-so-resonant absorption)

When the density gradient is STEEP (L_n ≲ v_osc/ω, where v_osc =
eE₀/m_eω is the electron quiver velocity), electrons at the critical
surface are pulled into vacuum during one laser half-cycle and slammed
back into the overdense plasma during the next. This "vacuum heating"
is intrinsically non-resonant.

**Absorption fraction** (Brunel 1987):
```
f_A ≈ (1/π) (v_osc³/c³) (ωL_n/v_osc)   [for v_osc/c ≲ 0.1]
```
Dominant for 10¹⁵ < Iλ² < 10¹⁷ W·μm²/cm² and L_n/λ ≲ 0.1.
Scales as ∝ I^{3/2} (super-linear — more efficient at higher I).

### 4. j×B heating (relativistic, a₀ > 1)

The v×B force oscillates at 2ω and drives density "bunches" at 2ω.
These couple to the laser via the ponderomotive force, producing
absorption even at NORMAL incidence (unlike resonance absorption).

**Absorption fraction** (Kruer-Estabrook 1985):
```
f_A ∝ a₀² I / n_c T_e    [scales with intensity, requires a₀ > 0.5]
```
Dominant for Iλ² > 10¹⁷ W·μm²/cm².

## Algorithm — Given (I, λ, T_e, L_n, Z, θ) → f_A

```
1. COMPUTE ν_ei. Compute α_IB. Compute collisional f_A.

2. CHECK if p-polarized + oblique: compute τ, compute f_A^res.

3. CHECK if L_n/λ ≪ 1 and v_osc/v_th > 1:
   Compute v_osc, f_A^Brunel.

4. CHECK if a₀ > 0.5: include j×B contribution.

5. TOTAL: f_A = max mechanisms (they generally don't add linearly
   — the dominant mechanism saturates the available energy).
   Transition hierarchy: collisional → resonance → Brunel → j×B
   with increasing Iλ².

6. REFLECTED energy: 1 − f_A. For ICF: need f_A > 0.8.
```

### Critical perspective on absorption formulas (High Power Laser-Matter Interaction 2010, Ch.2-3)

The textbook by Mulser & Bauer (2010) provides an important CRITICAL
perspective on standard absorption formulas, identifying several
limitations not covered by canonical derivations:

**Collisional absorption under strong drift**: the standard Dawson-Oberman
formula for ν_ei assumes a Maxwellian electron distribution. In intense
laser fields, the electron distribution develops a super-Gaussian tail
due to the quiver motion, reducing the effective collision frequency by
up to 30% compared to the Maxwellian assumption (HPLM Ch.3).

**Nonphysical asymptotic forms**: the product of two Coulomb logarithms
appearing in some asymptotic formulas for collisional absorption under
strong drift is an artifact of inconsistent approximations — the correct
form has a single lnΛ factor (HPLM §3.3.4). This affects absorption
calculations at I > 10¹⁶ W/cm² where the quiver velocity exceeds the
thermal velocity.

**Dimensional analysis and similarity** (HPLM Ch.2): the absorption
dynamics can be characterized by two dimensionless parameters:
```
Π = I / (n_e m_e c³)    [normalized intensity]
Λ = ν_ei L_n / c       [optical depth parameter]
```
These two parameters alone determine the absorption regime boundary,
enabling similarity scaling between experiments at different wavelengths
and intensities. This connects to `landau-graph: reasoning.dimensional_analysis_to_similarity`.

## Absorption Mechanism Regime Map

| Mechanism | Iλ² (W·μm²/cm²) | L_n/λ | Pol. | θ | Scaling |
|-----------|-----------------|-------|------|---|---------|
| Inverse bremsstrahlung | <10¹⁴ | any | any | any | ∝ n_e/T_e^{3/2} λ² |
| Resonance absorption | 10¹⁴–10¹⁶ | >1 | p | >0° | f_A ≈ ½ φ²(τ) |
| Brunel vacuum heating | 10¹⁵–10¹⁷ | <0.1 | p | >0° | ∝ (v_osc/c)³ |
| j×B heating | >10¹⁶ | any | any | any | ∝ a₀² |

## Edge Cases

- **α_IB divergence near n_c**: The formula α_IB ∝ 1/√(1−n_e/n_c) diverges as
  n_e → n_c. For n_e/n_c > 0.5, the WKB propagation model breaks down and
  α_IB is not physically meaningful. The actual absorption is limited by
  the finite density scale length L_n near the critical surface. Use the
  full wave solution or effective absorption efficiency ∝ L_n^{−1} ω/c.

- **Overlapping regimes**: At Iλ² ∼ 10¹⁵ near steep gradients, resonance
  absorption and Brunel heating coexist → full PIC needed.
- **Saturated absorption**: f_A cannot exceed 1. In practice f_A ≤ 0.8
  in most regimes due to reflection. Only in deep density cavities
  (ponderomotive hole-boring) can f_A → 1.
- **Hot electron generation**: Resonance absorption and Brunel heating
  produce suprathermal electrons with T_hot ≫ T_cold → preheat in ICF.

## Cross-References

- Kruer §3-4, Gibbon §3-4, Eliezer §4-5
- laser-plasma: reasoning.lp.laser_propagation_plasma (parent — n_c, turning point)
- laser-plasma: reasoning.lp.ponderomotive_force (hole boring, density steepening)
- laser-plasma: knowledge.lp.laser_absorption_data (numerical values)
