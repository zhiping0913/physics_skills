---
skill_id: reasoning.em.nonlinear_optical_response
type: reasoning
summary_50t: >
  Strong E: P = ε₀(χ⁽¹⁾E + χ⁽²⁾EE + χ⁽³⁾EEE + ...). χ⁽²⁾ → SHG, sum/difference
  frequency, Pockels. χ⁽³⁾ → Kerr, self-focusing, FWM. Phase matching Δk=0
  required. Manley-Rowe: photon number conservation in nonlinear mixing.
trigger:
  - laser fields strong enough that P ∝ E breaks down
  - frequency conversion (SHG, OPO, parametric amplification)
  - self-focusing, self-phase modulation in intense beams
reasoning_role: nonlinear_optics
parent: knowledge.continuous.dielectric_dispersion
retrieval_cost: 1
references:
  - landau-graph: knowledge.continuous.dielectric_dispersion
---

# reasoning.em.nonlinear_optical_response — Strong Field → Harmonic Generation

## Core Picture

At low intensities, P = ε₀χ⁽¹⁾E (linear optics). When E approaches atomic
field strengths (∼10¹¹ V/m), the anharmonicity of the binding potential
becomes significant → nonlinear polarization:

```
P_i = ε₀[χ⁽¹⁾_ij E_j + χ⁽²⁾_ijk E_j E_k + χ⁽³⁾_ijkl E_j E_k E_l + ...]
```

The nonlinear susceptibilities χ⁽ⁿ⁾ are tensors constrained by crystal
symmetry (same pattern as `reasoning.constitutive_relation_from_symmetry`).

## Second-Order Effects (χ⁽²⁾)

Requires non-centrosymmetric medium (χ⁽²⁾=0 in centrosymmetric crystals).

**Second Harmonic Generation (SHG)**: ω + ω → 2ω
Two pump photons → one frequency-doubled photon. Conversion efficiency η = I_{2ω}/I_ω.
For plane waves: η ∝ sinc²(Δk L/2) where Δk = k_{2ω} − 2k_ω.

**Phase matching**: For efficient SHG, Δk = 0 → n_ω = n_{2ω}. This NEVER
happens in isotropic media (normal dispersion: n_{2ω} > n_ω). Solution:
use BIREFRINGENT crystal where ordinary and extraordinary indices differ →
n_o(ω) = n_e(2ω) at specific angle θ_pm (Type I or Type II phase matching).

**Sum/difference frequency**: ω₁ + ω₂ → ω₃ (SFG), ω₁ − ω₂ → ω₃ (DFG).
Optical parametric oscillator (OPO): pump ω_p → signal ω_s + idler ω_i
with ω_p = ω_s + ω_i.

**Pockels effect**: χ⁽²⁾(ω; ω, 0) — DC field changes refractive index linearly.
n(E) = n₀ − (1/2)n₀³r_eff E. Used in electro-optic modulators.

## Third-Order Effects (χ⁽³⁾)

Allowed in ALL media (centrosymmetric included). Weaker than χ⁽²⁾ but universal.

**Kerr effect**: n = n₀ + n₂ I where n₂ ∝ Re[χ⁽³⁾]. Intensity-dependent
refractive index → self-phase modulation (SPM), self-focusing.

**Self-focusing**: Gaussian beam with n₂ > 0 → higher intensity on axis →
higher n → focusing. Critical power: P_cr ≈ λ²/(8πn₀n₂). For P > P_cr,
catastrophic self-focusing → filamentation or damage.

**Four-wave mixing (FWM)**: ω₁ + ω₂ → ω₃ + ω₄. Phase conjugation when
ω₄ = 2ω_p − ω_s (signal wave reversed).

## Manley-Rowe Relations

In lossless nonlinear mixing, photon number is conserved:
ΔN₁/ω₁ = ΔN₂/ω₂ = ... (energy flow between modes preserves total photon number).
This is a consequence of the time-averaged Hamiltonian structure.

## Connection to Strong-Field QED

When E approaches the Schwinger limit E_cr = m²c³/eℏ ≈ 1.3×10¹⁶ V/cm,
the VACUUM itself becomes nonlinear (vacuum polarization, pair production).
The effective Lagrangian: L = L_Maxwell + (α²/90m⁴)[(F²)² + 7(F·F̃)²] + ...
This is the Euler-Heisenberg effective action — nonlinear optics of the vacuum.

## Cross-References

- Avetissian §2-3 (nonlinear Compton, induced Cherenkov)
- Born & Wolf §12 (nonlinear optics basics)
- landau-graph: knowledge.continuous.dielectric_dispersion (linear regime)
- landau-graph: reasoning.constitutive_relation_from_symmetry (χ⁽ⁿ⁾ tensor symmetry)
- optics: reasoning.optics.pulse_propagation_nlse (γ from χ⁽³⁾ → Kerr coefficient
  n₂ feeds NLSE soliton formation; bidirectional: NLSE consumes this parent)
