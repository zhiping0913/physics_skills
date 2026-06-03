---
skill_id: reasoning.optics.pulse_propagation_nlse
type: reasoning
summary_50t: >
  ∂A/∂z=−iβ₂/2 ∂²A/∂T²−α/2 A+iγ|A|²A. GVD (β₂): normal→red leads blue,
  anomalous→compressible. SPM (γ): φ_NL=γP₀L. Soliton: N²=γP₀T₀²/|β₂|=1.
  Modulation instability for β₂<0. Self-steepening, Raman shift at few-cycle.
trigger: propagating ultrashort pulses in fiber/bulk, soliton formation
reasoning_role: nlse_propagation
parent: reasoning.em.nonlinear_optical_response
retrieval_cost: 1
---

# reasoning.optics.pulse_propagation_nlse — Dispersion + Nonlinearity → Pulse Evolution

## Core Picture

The Nonlinear Schrödinger Equation (NLSE) governs pulse propagation in
dispersive, nonlinear media (Boyd §7, Siegman §9-10). It balances GVD
(group-velocity dispersion, linear) with SPM (self-phase modulation,
nonlinear via Kerr effect n₂).

## Algorithm

```
1. NLSE (retarded time T = t − z/v_g, slowly-varying envelope A):
   ∂A/∂z = −i(β₂/2) ∂²A/∂T² − (α/2)A + iγ|A|²A

   β₂ = d²k/dω² (GVD). β₂>0 normal (red faster), β₂<0 anomalous.
   γ = n₂ ω₀/(c A_eff) (nonlinear coefficient). α = loss.

2. CHARACTERISTIC LENGTHS:
   Dispersion length: L_D = T₀²/|β₂|. Nonlinear length: L_NL = 1/(γP₀).
   L ≪ L_D, L ≪ L_NL: pulse unchanged. L ∼ L_D ≪ L_NL: GVD dominates.
   L ∼ L_NL ≪ L_D: SPM dominates. L ≳ both: NLSE balance.

3. GVD only (γ=0, α=0): A(z,T) = FT⁻¹{A(0,ω) exp(iβ₂ω²z/2)}.
   Gaussian: τ(z)=τ₀√[1+(z/L_D)²]. Chirp: Δω(z)=C z/L_D/(1+(z/L_D)²).

4. SPM only (β₂=0, α=0): A(z,T)=A(0,T) exp(iγ|A|²z).
   φ_NL = γP₀ L. Δω_max ∝ (γP₀/T₀)L. Spectrum broadens symmetrically.

5. GVD + SPM (soliton regime, β₂<0):
   SOLITON ORDER: N² = L_D/L_NL = γP₀T₀²/|β₂|.
   N=1: fundamental soliton, sech² shape, propagates indefinitely unchanged.
   N>1: periodic evolution with period z₀ = πL_D/2.

6. MODULATION INSTABILITY (β₂<0, CW or long pulse):
   Small perturbation ∝ exp(gz): g² = −(β₂Ω²/2)(β₂Ω²/2+2γP₀).
   Maximum gain at Ω_max = √(2γP₀/|β₂|), g_max = 2γP₀.
   CW breaks into pulse train → soliton fission.
```

## Higher-Order Effects (ultrashort, <100 fs)

- **TOD** (β₃): asymmetric pulse distortion, oscillatory tail.
- **Self-steepening** (∂/∂T(γ|A|²A)): pulse peak trails, shock formation.
- **Intrapulse Raman** (T_R): soliton self-frequency shift to longer λ.

## Edge Cases

- **Normal dispersion** (β₂>0): no bright soliton. Dark soliton (dip on CW).
  Requires NLS with defocusing nonlinearity.
- **Few-cycle**: envelope approximation breaks. Need full Maxwell + nonlinear
  polarization. Carrier-envelope phase becomes critical.

## Cross-References

- Boyd §7, Siegman §9-10, Agrawal (Nonlinear Fiber Optics)
- landau-graph: knowledge.continuous.dielectric_dispersion (β₂ from ε(ω))
- electrodynamics: reasoning.em.nonlinear_optical_response (parent: γ from χ⁽³⁾)
