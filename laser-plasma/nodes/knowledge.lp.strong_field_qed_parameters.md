---
skill_id: knowledge.lp.strong_field_qed_parameters
type: knowledge
summary_50t: >
  Strong-field QED reference data: Schwinger field E_cr = 1.32×10¹⁶ V/cm.
  χ parameter table for various laser/electron combinations. I_cr =
  4.6×10²⁹ W/cm². a₀_S = mc²/ℏω ≈ 4.1×10⁵ (optical). Photon emission
  spectrum (nonlinear Compton), pair production rate (Breit-Wheeler).
  Quantum suppression factor g(χ). QED-PIC code parameters.
trigger:
  - looking up χ for specific a₀, γ_e combinations
  - computing photon emission and pair production rates
parent: reasoning.lp.strong_field_qed_plasma
retrieval_cost: 1
---

# knowledge.lp.strong_field_qed_parameters — χ Tables & QED Data

## Fundamental QED Scales

| Parameter | Symbol | Value | Notes |
|-----------|--------|-------|-------|
| Schwinger field | E_cr | 1.32×10¹⁶ V/cm | m²c³/eℏ |
| Schwinger intensity | I_cr | 4.6×10²⁹ W/cm² | cE_cr²/8π |
| Critical B-field | B_cr | 4.4×10⁹ T | m²c²/eℏ |
| Compton wavelength | λ_C | 2.43×10⁻¹² m | ℏ/mc |
| Classical electron radius | r_e | 2.82×10⁻¹⁵ m | e²/mc² |
| Fine-structure constant | α | 1/137.036 | e²/ℏc |
| a₀ for pair production | a₀_S | 4.1×10⁵ (λ=1μm) | mc²/ℏω |

## χ Parameter Lookup Table

For electron with Lorentz factor γ in laser field a₀, λ₀:
```
χ_e = 2 γ a₀ (ℏω₀/mc²) = 3.8×10⁻⁶ γ a₀ (λ₀=0.8μm)
```

| a₀ | γ_e | χ_e (0.8μm) | Regime |
|----|-----|------------|--------|
| 1 | 10 | 3.8×10⁻⁴ | QED negligible |
| 10 | 100 | 0.038 | Weak QED: photon emission |
| 100 | 100 | 0.38 | Strong QED: frequent emission |
| 100 | 1000 | 3.8 | QED-dominated: pair production |
| 500 | 500 | 9.5 | QED cascade |
| 1000 | 100 | 3.8 | — |
| 10⁴ | 10⁴ | 380 | Vacuum pair production |

I corresponding to a₀ at 0.8 μm: I[W/cm²] = 1.37×10¹⁸ a₀².

## Photon Emission (Nonlinear Compton)

**Rate parameterization** (Erber 1966 / Ritus 1985):
```
dN_γ/dt = (α m c²/ℏ γ) · χ_e^{2/3} · K_{1/3}(2χ_e^{1/3}/3) / √3π
```

| χ_e | dN_γ/dt (γ=1000) | ℏω_γ typical |
|-----|-------------------|--------------|
| 0.01 | 10¹² s⁻¹ | — |
| 0.1 | 5×10¹⁴ s⁻¹ | 0.02 γ m c² |
| 1.0 | 2×10¹⁶ s⁻¹ | 0.07 γ m c² |
| 10 | 3×10¹⁷ s⁻¹ | 0.15 γ m c² |

**Photon energy spectrum** (differential rate):
```
d²N/d(ℏω)dt ∝ χ_e^{2/3} (ℏω/γmc²)^{-2/3} exp(−2ℏω/3χ_e γ m c²)
```

## Pair Production (Breit-Wheeler)

**Photon with energy ℏω in field a₀**:
```
χ_γ = (ℏω/mc²)(a₀ ℏω₀/mc²)    [counter-propagating photon]
     = (ℏω/mc²)(a₀ × 1.96×10⁻⁶)   [λ₀=0.8μm]
```

| ℏω | a₀ | χ_γ | Pair probability |
|----|----|-----|-----------------|
| 1 MeV | 100 | 3.8×10⁻³ | Negligible |
| 100 MeV | 100 | 0.38 | ~10⁻³ per λ₀ |
| 1 GeV | 100 | 3.8 | ~0.1 per λ₀ |
| 100 MeV | 500 | 1.9 | ~0.01 per λ₀ |

**Rate**: per unit time for a photon in the laser field:
```
Γ_BW ≈ (α m²c⁴/ℏ²ω) χ_γ K_{1/3}²(4/3χ_γ)    [χ_γ ≪ 1]
Γ_BW ≈ 0.38 α m c² χ_γ^{2/3} / ℏ ω           [χ_γ ≫ 1]
```

## Quantum Suppression Factor

Classical vs quantum radiated power ratio:
```
g(χ) ≡ P_quantum / P_classical
g(χ) ≈ 1 / (1 + 4.8 χ_e^{1.25} + 3.6 χ_e^{2.0})
```

| χ_e | g(χ) | Suppression |
|-----|------|------------|
| 0.01 | 0.95 | 5% |
| 0.1 | 0.67 | 33% |
| 0.5 | 0.35 | 65% |
| 1.0 | 0.17 | 83% |
| 5.0 | 0.023 | 98% |
| 10 | 6.7×10⁻³ | 99.3% |

## QED-PIC Code Parameters

| Code | QED module | Methods |
|------|-----------|---------|
| EPOCH | Yes | MC emission + BW, spin |
| PIConGPU | Yes | MC emission + BW |
| OSIRIS | Yes | MC emission + BW, spin |
| SMILEI | Yes | MC emission + BW |
| VLPL | Yes | MC emission + BW, cascades |
| WarpX | Planned | Boosted frame + QED |

**MC sub-stepping**: when dN_γ/dt × Δt > 1 → sub-divide timestep
to capture individual emission events. Typical: 10–100 sub-steps
at χ_e ~ 1.

## Cross-References

- laser-plasma: reasoning.lp.strong_field_qed_plasma (parent — theory)
- laser-plasma: reasoning.lp.radiation_reaction (χ ⟷ R_c)
- laser-plasma: knowledge.lp.plasma_parameters_laser (I ↔ a₀)
