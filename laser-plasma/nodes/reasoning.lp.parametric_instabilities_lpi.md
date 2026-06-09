---
skill_id: reasoning.lp.parametric_instabilities_lpi
type: reasoning
summary_50t: >
  Three-wave parametric instabilities in LPI: SRS (laser→scattered light
  + plasma wave), SBS (laser→scattered light + ion acoustic wave), TPD
  (laser→two plasma waves at ω_p). Frequency matching: ω₀=ω₁+ω₂,
  k-matching: k₀=k₁+k₂. Rosenbluth convective gain, absolute threshold.
  SRS: growth γ₀=(k_epw v_osc/4)√(ω_p/ω₀). SBS: γ₀=(k_iaw v_osc/4).
  Saturation: pump depletion, ion trapping, Langmuir decay instability.
trigger:
  - computing SRS/SBS/TPD thresholds and growth rates for ICF
  - analyzing backscatter losses in laser-plasma coupling
  - distinguishing absolute vs convective instability regimes
reasoning_role: parametric_instabilities
parent: reasoning.plasma.dispersion_relation_method
retrieval_cost: 1
sign_convention: >
  ω₀ = pump (laser) frequency. ω₁,ω₂ = daughter wave frequencies.
  k₀,k₁,k₂ = wavevectors with k₀ = k₁ + k₂. SRS: ω₁ ≈ ω₀−ω_p (scattered EM),
  ω₂ ≈ ω_p (EPW). SBS: ω₁ ≈ ω₀−ω_iaw (scattered EM), ω₂ = ω_iaw (IAW).
  TPD: ω₁ ≈ ω₂ ≈ ω_p = ω₀/2. Growth rate γ in s⁻¹ or m⁻¹ (convective).
---

# reasoning.lp.parametric_instabilities_lpi — Three-Wave Coupling → SRS/SBS/TPD

## Core Picture

An intense laser pump (ω₀,k₀) in plasma can decay into two daughter waves
(ω₁,k₁) and (ω₂,k₂) via resonant three-wave coupling. The three canonical
instabilities in laser-plasma interaction are Stimulated Raman Scattering
(SRS: laser → scattered EM + electron plasma wave), Stimulated Brillouin
Scattering (SBS: laser → scattered EM + ion acoustic wave), and Two-Plasmon
Decay (TPD: laser → two electron plasma waves near n_c/4). These are the
dominant mechanisms for laser energy reflection and hot electron generation
in ICF (Kruer §7-9, HPP-3 §4, Gibbon §4).

## Derivation Sketch

### 1. Three-wave coupling equations

For a pump (ω₀,k₀) driving daughter waves (ω₁,k₁), (ω₂,k₂) with slowly
varying amplitudes a₁, a₂:
```
(∂_t + v_g1·∇ + ν₁) a₁ = γ₀ a₂*
(∂_t + v_g2·∇ + ν₂) a₂ = γ₀ a₁*
```
Frequency and wavevector matching:
```
ω₀ = ω₁ + ω₂,    k₀ = k₁ + k₂
```
γ₀ is the homogeneous growth rate (infinite plasma, no damping):
```
γ₀² = (coupling coefficient) × (pump intensity)
```

### 2. Stimulated Raman Scattering (SRS)

**Decay**: Laser (ω₀) → scattered EM wave (ω_s = ω₀−ω_p) + electron plasma wave (ω_p).

**Phase matching**: k₀ = k_s + k_epw. Backscatter (k_s ≈ −k₀):
```
k_epw = k₀ − k_s ≈ 2k₀  [forward scatter: k_epw ≈ 0]
```

**Homogeneous growth rate** (backscatter, n_e ≪ n_c):
```
γ₀ = (k_epw v_osc/4) √(ω_p/ω_s)
```
where v_osc = eE₀/m_eω₀ is the electron quiver velocity.
In terms of a₀: γ₀/ω₀ ≈ (a₀/4) √(n_e/n_c).

**Density dependence**: SRS grows at n_e < n_c/4 (above n_c/4, ω_p > ω₀/2
and the scattered wave becomes evanescent). Maximum at n_e ≈ n_c/4.

**Convective gain** for length L (Rosenbluth):
```
G = 2π γ₀² L / (|v_g1 v_g2| κ')    [convective amplification]
```
where κ' is the wavevector mismatch derivative. Practical: G > 10 for
significant SRS.

**Absolute instability**: at n_c/4 where v_g1 ≈ v_g2 → waves trapped →
feedback → absolute growth. Threshold: γ₀ > √(ν₁ν₂).

### 3. Stimulated Brillouin Scattering (SBS)

**Decay**: Laser (ω₀) → scattered EM wave (ω_s ≈ ω₀) + ion acoustic wave (ω_iaw).

**Homogeneous growth rate** (backscatter):
```
γ₀ = (k_iaw v_osc/4) √(n_e/n_c) (ω_p/ω_iaw)
```
SBS growth rate is typically LOWER than SRS because ω_p/ω_iaw ∼ √(m_i/Zm_e) ≫ 1
is offset by the small IAW coupling. But SBS can operate at ALL densities
n_e < n_c (no n_c/4 cutoff).

**Convective gain** similar to SRS but with IAW group velocity (much smaller
than EPW → potentially larger gain per unit length).

### 4. Two-Plasmon Decay (TPD)

**Decay**: Laser (ω₀) → two electron plasma waves, each at ω₀/2.

**Condition**: n_e ≈ n_c/4 so that ω_p ≈ ω₀/2.
```
γ₀ = (k_epw v_osc/4)    [homogeneous growth rate at exact n_c/4]
```
TPD produces plasma waves that can trap and accelerate electrons → hot
electron preheat in ICF. Absolute threshold: γ₀ > √(ν_EPW ν_EPW).

### 5. Instability saturation mechanisms

| Instability | Primary saturation | Threshold for saturation |
|------------|-------------------|------------------------|
| SRS | Pump depletion, EPW breaking, Langmuir decay instability (LDI) | δn/n > 0.1 |
| SBS | Ion trapping, pump depletion | δn/n > 1 (large-amplitude IAW) |
| TPD | EPW breaking, pump depletion | eE_epw/m_eω_p > v_th |

## Algorithm — Given (I, λ, n_e, T_e, L, Z) → Growth Rates/Thresholds

```
1. COMPUTE v_osc = eE₀/m_eω, a₀ = v_osc/c.

2. SRS:
   - Check n_e < n_c/4. If not, SRS forbidden.
   - Compute k_epw ≈ 2ω₀/c for backscatter.
   - γ₀ = (k_epw v_osc/4) √(ω_p/ω₀−ω_p).
   - ν_EPW ≈ Landau damping rate.
   - Convective gain: G = 2πγ₀²L/(|v_g1 v_g2|κ').

3. SBS:
   - Compute ω_iaw = k_iaw c_s with c_s = √(ZT_e/m_i).
   - γ₀ = (k_iaw v_osc/4) √(n_e/n_c) (ω_p/ω_iaw).
   - ν_IAW ≈ ν_ii (ion Landau damping).
   - Check for absolute growth at high gain.

4. TPD:
   - Check n_e ≈ n_c/4. γ₀ = k_epw v_osc/4.
   - Absolute threshold: γ₀ > ν_EPW.

5. DETERMINE dominant instability: highest growth rate given
   density and temperature.
```

## Instability Parameter Table

| Inst. | n_e range | ω matching | Daughter waves | Backscatter γ₀/ω₀ | Saturation |
|-------|----------|-----------|---------------|-------------------|------------|
| SRS | <n_c/4 | ω₀ = ω_s + ω_epw | EM + EPW | (a₀/4)√(n_e/n_c) | LDI, EPW breaking |
| SBS | <n_c | ω₀ = ω_s + ω_iaw | EM + IAW | a₀/4 · small factor | Ion trapping |
| TPD | ≈n_c/4 | ω₀ = ω_p + ω_p | EPW + EPW | k_epw v_osc/4 | EPW breaking |

## Edge Cases

- **SRS in inhomogeneous plasma**: density gradient detunes the resonance →
  convective gain reduced. Phase matching maintained only over ~L_res.
- **Kinetic effects**: When k_epw λ_D > 0.3, Landau damping strongly
  suppresses SRS → nonlinear kinetic regime (particle trapping dominant).
- **Multi-speckle SRS**: In smoothed laser beams, SRS grows in individual
  speckles → statistical treatment needed.

## Cross-References

- Kruer §7-9, HPP-3 §4, Gibbon §4
- plasma: reasoning.plasma.dispersion_relation_method (parent — three-wave coupling)
- plasma: reasoning.plasma.instability_classification (absolute vs convective)
- laser-plasma: reasoning.lp.laser_absorption_mechanisms (absorption competes with instabilities)
- laser-plasma: knowledge.lp.parametric_instability_data (threshold values)
