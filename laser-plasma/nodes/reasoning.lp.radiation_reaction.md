---
skill_id: reasoning.lp.radiation_reaction
type: reasoning
summary_50t: >
  Radiation reaction force on accelerating electrons: classical (Landau-
  Lifshitz) f_RR ≈ (2e³/3mc³) γ² a² vs quantum (stochastic photon emission).
  Radiation-dominated regime: R_c = α χ_e a₀ ≫ 1 → electron loses most energy
  to radiation. Modified Lorentz equation: dp^μ/dτ = (e/m)F^{μν}p_ν + f_RR^μ.
  Observable: electron energy clamping, beam cooling, synchrotron radiation.
trigger:
  - determining when radiation reaction modifies electron dynamics
  - choosing classical vs quantum radiation reaction model
  - interpreting electron spectra from high-intensity experiments
reasoning_role: radiation_reaction
parent: reasoning.lp.strong_field_qed_plasma
retrieval_cost: 1
sign_convention: >
  Lorentz-Abraham-Dirac (LAD): pathological pre-acceleration. Landau-Lifshitz
  (LL): reduced-order approximation, causal. Quantum: stochastic emission.
  R_c = α χ_e a₀ = radiation dominance parameter.
---

# reasoning.lp.radiation_reaction — Energy Loss → Modified Dynamics

## Core Picture

Accelerating charges radiate. For electrons in ultra-intense laser fields
(a₀ ≫ 1, γ ≫ 1), the radiated power becomes comparable to the power gained
from the laser field — radiation reaction (RR) fundamentally alters the
electron trajectory and energy spectrum. In the CLASSICAL regime, RR is
described by the Landau-Lifshitz (LL) equation. In the QUANTUM regime
(χ_e ≳ 0.1), photon emission is stochastic and discrete, requiring Monte
Carlo treatment. The radiation-dominated regime (R_c ≫ 1) is where RR
dominates electron dynamics — accessible at I > 10²³ W/cm²
(Di Piazza 2008, Bulanov et al. 2011, Cole et al. 2018).

## Derivation Sketch

### 1. Larmor power — the radiation source

Electron radiated power in the instantaneous rest frame:
```
P = (2e²/3c³) a²    [Larmor formula]
```
In the lab frame (relativistic, with acceleration a_lab):
```
P_lab = (2e²/3c) γ² [a²_lab − (v×a_lab)²/c²]
```

For an electron in a strong laser field (a_lab ≈ eE₀/γ m_e for a₀ ≫ 1):
```
P_lab ≈ (2e²/3c) (eE₀/m_e)² γ² ≈ (2α/3) m_e c² ω₀ χ_e γ
```
where α = e²/(4πε₀ℏc) ≈ 1/137.

The fraction of electron energy lost per laser period:
```
δγ/γ ≈ P_lab T₀ / (γ m_e c²) ≈ α χ_e a₀ = R_c
```
where R_c ≡ α χ_e a₀ is the **radiation dominance parameter**.

### 2. Classical radiation reaction — Landau-Lifshitz

The Lorentz-Abraham-Dirac (LAD) equation:
```
m du^μ/dτ = (e/c) F^{μν} u_ν + (2e²/3c³)(d²u^μ/dτ² + u^μ u^ν d²u_ν/dτ²)
```
LAD contains pre-acceleration (pathological runaway solutions).

**Landau-Lifshitz approximation** (reducing LAD order by substituting
d²u/dτ² from the Lorentz force):
```
f_RR^μ = (2e³/3mc⁴) [∂_α F^{μν} u_ν u^α + (e/mc²) (F^{μα} F_{αν} u^ν
         + (F_{να} u^α)(F^{νβ} u_β) u^μ)]
```

For a plane wave, the dominant term is the radiative damping force:
```
f_RR ≈ −(2e⁴/3m²c⁶) γ² E_lab² v/c    [anti-parallel to velocity]
```

The LL equation is valid for χ_e ≪ 1 and when the radiation wavelength
is much larger than the Compton wavelength λ ≫ λ_C = ℏ/mc.

### 3. Quantum radiation reaction

For χ_e ≳ 0.1, photon emission is inherently quantum:
- Emission is STOCHASTIC (not continuous).
- Each photon carries ∼ χ_e γ m c² energy → large fractional energy changes.
- The recoil from a single photon emission can be significant.

The quantum-corrected RR is modeled via **Monte Carlo emission**:
1. At each timestep, compute emission probability from QED rate.
2. Sample photon energy from the nonlinear Compton spectrum.
3. Update electron momentum with recoil.

**Quantum reduction in total radiated power** (compared to classical):
```
P_quantum / P_classical ≈ g(χ_e) where g(χ) ≈ 1/(1+4.8χ^{1.25})
```
At χ_e = 1: g ≈ 0.17 → quantum suppression reduces radiated power ~6×.

### 4. Radiation-dominated regime

When R_c = α χ_e a₀ ≫ 1:
- The electron loses most of its energy within one laser period.
- γ is "clamped": γ_max ≈ a₀ / (α χ_e)^{1/3}.
- Direct laser acceleration (DLA) is suppressed — electrons radiate
  before gaining significant energy.
- The electron motion transitions from "acceleration-dominated" to
  "radiation-dominated" dynamics.

**Phase diagram**:
| R_c | Regime | Behavior |
|-----|--------|----------|
| ≪ 0.01 | RR negligible | Lorentz force only |
| 0.01–0.1 | Weak RR | Small energy loss per period |
| 0.1–1 | Moderate RR | Significant damping |
| 1–10 | Strong RR | γ clamped, DLA suppressed |
| ≫ 10 | Radiation-dominated | Electron trajectory determined by RR |

### 5. Experimental signatures

- **Energy clamping**: electron spectra show a cutoff at γ ∼ a₀/(αχ)^{1/3}
  instead of continuing to γ ∼ a₀².
- **Radiation cooling**: electron beam emittance decreases (unusual —
  normally acceleration increases emittance).
- **Gamma-ray beam generation**: the radiated photons form a collimated
  beam → bright γ-ray source.
- **Pair production seeding**: the emitted γ photons initiate QED cascades.

## Algorithm — Given (a₀, γ_e, λ₀) → Radiation Reaction Regime

```
1. COMPUTE χ_e ≈ 2γ_e a₀ (ℏω₀/mc²).

2. COMPUTE R_c = α χ_e a₀.
   α = 1/137. R_c ≈ 5.3×10⁻⁵ γ_e a₀² for λ₀=0.8μm.

3. RR MODEL:
   R_c < 0.01: ignore RR (Lorentz force only).
   0.01 < R_c < 1, χ_e < 0.1: classical LL equation.
   χ_e > 0.1: quantum Monte Carlo (stochastic emission).

4. ENERGY LOSS per laser period:
   δγ_loss ≈ R_c γ.
   δγ_gain ≈ a₀ (from laser acceleration).
   Net: δγ ≈ a₀ − R_c γ.

5. SATURATED γ: γ_sat ≈ a₀ / R_c ≈ (137 a₀) / (a₀²) ∼ 10⁴/a₀.
```

## Edge Cases

- **Vacuum vs plasma**: in vacuum, RR is the only dissipation. In plasma,
  collective effects (wakefield, beam loading) compete with RR.
- **Spin polarization**: quantum RR with spin → Sokolov-Ternov effect →
  asymmetric photon emission → electron beam self-polarization.
- **RR modification of LWFA**: at extreme intensities, RR damping in the
  bubble may reduce the accelerating gradient.

## Cross-References

- Di Piazza, PLA 2008 — Landau-Lifshitz radiation reaction
- Cole et al., PRX 2018 — experimental evidence for RR
- Bulanov et al., PPCF 2011 — radiation-dominated regime
- laser-plasma: reasoning.lp.strong_field_qed_plasma (parent — QED context for RR)
- laser-plasma: reasoning.lp.laser_wakefield_acceleration (RR modifies LWFA)
- electrodynamics: reasoning.em.radiation_fields (Larmor formula derivation)
