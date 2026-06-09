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
sign_convention: >
  NLSE with retarded time T = t − z/v_g. β₂>0: normal GVD. β₂<0: anomalous.
  γ>0 for self-focusing Kerr (χ⁽³⁾>0). N² = L_D/L_NL = γP₀T₀²/|β₂|.
---

# reasoning.optics.pulse_propagation_nlse — Dispersion + Nonlinearity → Pulse Evolution

## Core Picture

The Nonlinear Schrödinger Equation (NLSE) governs pulse propagation in
dispersive, nonlinear media (Boyd §7, Siegman §9-10, Agrawal §2). It balances
GVD (group-velocity dispersion, linear) with SPM (self-phase modulation,
nonlinear via Kerr effect n₂).

## Derivation Sketch (from Maxwell + χ⁽³⁾ → NLSE)

Starting from `electrodynamics: reasoning.em.nonlinear_optical_response`
(χ⁽³⁾ tensor → Kerr nonlinearity):

1. **Wave equation in nonlinear medium** (Boyd §2):
   ∇²E − (n₀²/c²)∂²E/∂t² = μ₀ ∂²P_NL/∂t²
   where P_NL = ε₀ χ⁽³⁾ |E|² E (Kerr term, isotropic medium). Only the
   frequency component near ω₀ is retained (rotating-wave approximation).

2. **Slowly-varying envelope ansatz** (SVEA):
   E(z,t) = ½ A(z,t) exp[i(k₀z − ω₀t)] + c.c.
   Assume ∂A/∂z ≪ k₀A and ∂A/∂t ≪ ω₀A. Neglect ∂²A/∂z².

3. **Expand k(ω) around ω₀** (from `landau-graph: knowledge.continuous.dielectric_dispersion`):
   k(ω) = k₀ + β₁(ω−ω₀) + (β₂/2)(ω−ω₀)² + ...
   β₁ = dk/dω = 1/v_g,   β₂ = d²k/dω² = GVD.

4. **Retarded time frame**: T = t − z/v_g. Replace (ω−ω₀) → i∂/∂T via
   Fourier transform correspondence. Drop second derivatives of envelope
   and terms ∝ (∂²A/∂T²)∂A/∂z (small).

5. **Result — NLSE**:
   ∂A/∂z = −i(β₂/2) ∂²A/∂T² + iγ|A|²A
   with γ = n₂ ω₀ / (c A_eff),   n₂ = (3 / 4n₀² ε₀ c) Re[χ⁽³⁾₁₁₁₁].
   **This is the bridge to the parent χ⁽³⁾ node**: γ expresses the Kerr
   nonlinearity in terms of the nonlinear susceptibility. Isotropic Kerr
   reduces χ⁽³⁾_(ijkl) to a single independent component χ⁽³⁾₁₁₁₁.

   Including loss α: add −(α/2)A on RHS.

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
   Input: A(0,T) = √P₀ exp[−(1+iC)T²/(2T₀²)].
   C = chirp parameter (C>0: up-chirp, C<0: down-chirp; C=0: TL).
   Gaussian: τ(z) = τ₀√[1+(z/L_D)²]. Chirp: Δω(z)=C z/L_D/(1+(z/L_D)²).

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

## Dark Soliton (β₂>0 normal GVD, or defocusing γ<0)

For anomalous GVD β₂<0 with defocusing nonlinearity γ<0, OR normal GVD
β₂>0 with focusing γ>0 (equivalent via A→A* substitution):
```
  A(z,T) = √P₀ tanh(T/T₀)                                      (dark soliton)
```
The tanh profile is a "dip" on a CW background. Phase jump Δφ = π at T=0.
Gray soliton: depth parameter 0<η<1, A = √P₀ [cos φ₀ tanh(ηT/T₀)+i sin φ₀].
NLS with defocusing supports dark solitons but NOT bright solitons.

## XPM and Coupled NLSE

Coupled NLSE for two polarization/frequency channels (j=1,2):
  ∂A_j/∂z = −i(β₂j/2)∂²A_j/∂T² + iγ_j(|A_j|² + 2|A_{3−j}|²)A_j
XPM factor 2: incoherent cross-phase modulation (energy of field 2 modulates index seen by field 1).

**Plasma analog — relativistic self-focusing**: In plasma, n(I) = n₀ − n₂ I where
n₂ = −1/(2 n₀ a₀²) is the relativistic correction (a₀ = eE/(mωc)). Same I-dependence
as Kerr but PHYSICAL ORIGIN is mass increase, not bound-electron anharmonicity.
Cross-ref: `plasma: reasoning.lp.laser_propagation_plasma` (relativistic
self-focusing, critical power P_c = 17 (n_c/n_e) GW).

Also: self-steepening already in Higher-Order Effects section is fine. For the
vector NLSE (Manakov): add one line in the existing "#Vector NLSE" edge case:
"In fiber, polarization-averaged Manakov equation with 8/9 factor appears when
birefringence beat length ≪ nonlinear length. Cross-ref to `reasoning.plasma.dielectric_tensor_magnetized`
for 2×2 coupled-mode structure with plasma R/L waves."

## Higher-Order Effects (ultrashort, <100 fs)

- **TOD** (β₃): asymmetric pulse distortion, oscillatory tail.
- **Self-steepening**: (i/ω₀)∂/∂T(γ|A|²A) term. Pulse peak lags, optical
  shock formation. Derivation: expand χ⁽³⁾(ω) including first derivative.
- **Intrapulse Raman** (T_R): delayed nonlinear response → soliton
  self-frequency shift to longer λ (Δω ∝ −T_R τ⁻⁴).

## Edge Cases

- **Few-cycle pulses**: envelope approximation breaks. Use generalized NLSE
  with self-steepening term (1 + i/ω₀ ∂/∂T)(γ|A|²A), or the **forward
  Maxwell equation** (UPPE — unidirectional pulse propagation equation)
  for true few-cycle: ∂E(z,ω)/∂z = i[k(ω)−ω/v_g]E + i(μ₀ω²/2k)P_NL.
  Reference: Brabec & Krausz, PRL 78, 3282 (1997); Boyd §7.4.
  Carrier-envelope phase becomes critical.

- **Vector NLSE** (birefringent fiber): two coupled equations for x,y
  polarizations with XPM term 2iγ|A_⊥|²A_∥. In fiber, polarization-averaged
  Manakov equation with 8/9 factor appears when birefringence beat length
  ≪ nonlinear length. Cross-ref to `reasoning.plasma.dielectric_tensor_magnetized`
  for 2×2 coupled-mode structure with plasma R/L waves.

## Cross-References

- Boyd §7, Siegman §9-10, Agrawal (Nonlinear Fiber Optics) §2-5
- landau-graph: knowledge.continuous.dielectric_dispersion (β₂ from ε(ω))
- electrodynamics: reasoning.em.nonlinear_optical_response (parent: γ from χ⁽³⁾;
  Derivation Sketch step 5 consumes this parent explicitly)
- optics: reasoning.optics.dispersion_management_gdd (β₂ in NLSE IS GDD/L
  managed by gratings/prisms; cross-ref is bidirectional)
