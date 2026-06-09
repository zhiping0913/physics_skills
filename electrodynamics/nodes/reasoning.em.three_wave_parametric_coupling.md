---
skill_id: reasoning.em.three_wave_parametric_coupling
type: reasoning
summary_50t: >
  Generic three-wave parametric coupling: pump (ω₀,k₀) → daughter waves
  (ω₁,k₁)+(ω₂,k₂) with ω₀=ω₁+ω₂, k₀=k₁+k₂. Coupled-mode equations:
  ∂_t a₁ + v_g1·∇a₁ + ν₁a₁ = −iκ a₀ a₂*, ∂_t a₂ + v_g2·∇a₂ + ν₂a₂ =
  −iκ a₀ a₁*. Manley-Rowe invariants. Rosenbluth convective gain.
  Abstract skeleton shared by SRS/SBS/TPD (plasma), stimulated Raman/
  Brillouin (optics), OPA/OPO (nonlinear optics), and phonon-polariton
  coupling (condensed matter).
trigger:
  - recognizing 3-wave coupling in any physical domain
  - computing parametric growth rates from coupling coefficient
  - distinguishing absolute vs convective instability from group velocities
reasoning_role: three_wave_coupling
parent: reasoning.em.nonlinear_optical_response
retrieval_cost: 1
sign_convention: >
  ω₀ > ω₁ ≥ ω₂. κ = nonlinear coupling coefficient (units s⁻¹ or m⁻¹).
  v_g = group velocity. ν = damping rate. Convective: wave packets advect
  out of interaction region. Absolute: waves trapped → feedback → growth
  at fixed position.
---

# reasoning.em.three_wave_parametric_coupling — Generic Three-Wave Skeleton

## Core Picture

When an intense pump wave (ω₀,k₀) propagates through a nonlinear medium,
it can decay into two daughter waves (ω₁,k₁) and (ω₂,k₂) via resonant
three-wave coupling. The frequency and wavevector matching conditions
ω₀ = ω₁ + ω₂, k₀ = k₁ + k₂ define the resonant manifold. The growth
rate γ₀ is proportional to the pump amplitude and the nonlinear coupling
coefficient κ, which encodes the specific physics of each domain.

This node captures the SHARED mathematical skeleton. Domain-specific
nodes supply the coupling coefficient κ(domain parameters).

## Derivation Sketch

### 1. Coupled-mode equations

For slowly-varying amplitudes a₁, a₂ in the presence of undepleted pump a₀:
```
(∂_t + v_g1·∇ + ν₁) a₁ = −i κ a₀ a₂*
(∂_t + v_g2·∇ + ν₂) a₂ = −i κ a₀ a₁*
```
The coupling coefficient κ ∝ χ⁽²⁾ (second-order nonlinear susceptibility)
in the generalized sense: whatever physical mechanism couples the three waves.

### 2. Homogeneous growth rate

In a uniform medium with no damping (ν₁=ν₂=0):
```
γ₀ = |κ a₀|
```
This is the temporal growth rate (s⁻¹). The spatial growth rate is
γ₀/√(v_g1 v_g2) for counter-propagating geometry, γ₀/(v_g1 v_g2)^{1/2}

The growth rate scales linearly with pump amplitude — the hallmark of
parametric (as opposed to 4-wave/modulational) instability.

### 3. Frequency and wavevector matching

```
ω₀(k₀) = ω₁(k₁) + ω₂(k₂)    [conservation of energy]
k₀ = k₁ + k₂                 [conservation of momentum]
```

These define a resonant surface in (k₁,k₂) space. Solutions exist only
when the linear dispersion relations ω_i(k) permit simultaneous
satisfaction of both conditions.

### 4. Convective vs absolute instability

The character of the instability is determined by the group velocities:

- **Convective**: v_g1 × v_g2 > 0 (same sign) OR the interaction region
  is finite. Disturbances advect out of the pump region. Spatial growth
  characterized by convective gain exponent G.

- **Absolute**: v_g1 × v_g2 < 0 (opposite signs) AND the growth rate
  exceeds the wave-packet escape rate. Disturbances grow in place →
  feedback → self-sustained oscillation.

**Rosenbluth convective gain** (for weakly inhomogeneous medium):
```
G = 2π γ₀² L / (|v_g1 v_g2| κ')    [amplification factor]
```
where L is the interaction length and κ' = d(k₀−k₁−k₂)/dx is the
wavevector mismatch gradient. Significant growth for G > π.

### 5. Manley-Rowe relations

Photon-number conservation (quantum form):
```
N₁ + N₀ = const,    N₂ + N₀ = const,    N₁ − N₂ = const
```
where N_i = (energy in wave i) / ℏω_i. Each pump photon decays into exactly
one photon of each daughter wave — the quantum origin of parametric coupling.

### 6. Saturation mechanisms

| Mechanism | Condition | Effect |
|-----------|----------|--------|
| Pump depletion | a₀² ≈ a₁² + a₂² | γ₀ → 0 |
| Wave breaking | δn/n > 0.1 | Daughter wave cascades |
| Detuning | ∫κ' dx ≠ 0 | Phase mismatch accumulation |
| Particle trapping | ω_bounce > ν | Quasi-linear flattening |

## Domain-Specific Specializations

| Domain | Pump (ω₀) | ω₁ | ω₂ | κ (coupling) | Node |
|--------|----------|----|----|---------------|------|
| Laser-plasma SRS | Laser | Scattered EM | EPW (ω_p) | (e k_epw/4mω₀)E₀√(ω_p/ω_s) | lp.R4 |
| Laser-plasma SBS | Laser | Scattered EM | IAW (ω_iaw) | (e k_iaw/4mω₀)E₀√(ω_p/ω_iaw) | lp.R4 |
| Laser-plasma TPD | Laser | EPW (ω₀/2) | EPW (ω₀/2) | (e k_epw/4mω₀)E₀ | lp.R4 |
| Fiber SRS | Pump λ_p | Stokes λ_s | Optical phonon Ω_R | g_R (Raman gain) | optics.SRS |
| Fiber SBS | Pump | Stokes | Acoustic phonon Ω_B | g_B (Brillouin gain) | optics.SRS |
| OPA/OPO | Pump (ω_p) | Signal (ω_s) | Idler (ω_i) | χ⁽²⁾ | optics.parametric |
| Phonon-polariton | Laser | Lower polariton | Upper polariton | χ⁽²⁾ | — |

## Algorithm — Given (ω₀(k), κ, v_g1, v_g2, ν₁, ν₂) → Instability Properties

```
1. COMPUTE resonant (k₁,k₂) from frequency/wavevector matching.

2. GROWTH RATE: γ₀ = |κ a₀| (homogeneous, no damping).

3. CHECK convective vs absolute:
   If v_g1 × v_g2 < 0 AND γ₀ > √(ν₁ ν₂): absolute.
   Else: convective, compute G = 2π γ₀² L/(|v_g1 v_g2| κ').

4. THRESHOLD: G > π for observable convective amplification.

5. SATURATION: whichever mechanism has lowest threshold.
```

## Edge Cases

- **Degenerate daughters** (ω₁ ≈ ω₂): TPD is the degenerate case where
  the two daughter waves are identical → coupling coefficient differs by √2.
- **Backscatter vs forward scatter**: k₁ ≈ −k₀ (backscatter) → k₂ ≈ 2k₀,
  maximizing growth rate but also maximizing wavevector mismatch sensitivity.
  k₁ ≈ k₀ (forward scatter) → k₂ ≈ 0 → reduced growth but more robust matching.
- **Non-resonant coupling**: when detuning Δω = ω₀−ω₁−ω₂ ≠ 0, the growth
  rate is reduced: γ = √(γ₀² − Δω²/4). For Δω > 2γ₀: no growth.

## Cross-References

- electrodynamics: reasoning.em.nonlinear_optical_response (parent — χ⁽²⁾ basis)
- plasma: reasoning.plasma.instability_classification (convective/absolute framework)
- laser-plasma: reasoning.lp.parametric_instabilities_lpi (SRS/SBS/TPD — specialization)
- optics: reasoning.optics.stimulated_raman_scattering (fiber SRS/SBS — specialization)
