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
parent: landau-graph:knowledge.continuous.dielectric_dispersion
sign_convention: time-harmonic e^{−iωt}; SVEA with slowly-varying envelope A(z); P_i = ε₀χ⁽¹⁾_ij E_j + ε₀χ⁽²⁾_ijk E_j E_k + ...
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

## Derivation Sketch

Starting from `landau-graph: knowledge.continuous.dielectric_dispersion` we have
the linear response P(ω) = ε₀χ⁽¹⁾(ω)E(ω) — the material polarization responds
proportionally to the driving field at the same frequency. When E becomes
comparable to the atomic field E_at ≈ e/a₀² ≈ 5×10¹¹ V/m, the anharmonic
terms in the electron binding potential become significant.

**Key non-obvious step — coupled-wave equations from SVEA**:
The nonlinear wave equation ∇²E − (1/c²)∂²E/∂t² = μ₀∂²P_NL/∂t² is NOT
trivial to solve because P_NL couples waves at DIFFERENT frequencies.
The slowly-varying envelope approximation (SVEA) separates fast oscillations
from slow amplitude evolution. For SHG with E_ω(z) = A_ω(z)e^{i(k_ω z−ωt)}
and E_{2ω}(z) = A_{2ω}(z)e^{i(k_{2ω}z−2ωt)}:

```
dA_ω/dz   = i(ω²/2k_ωc²) χ⁽²⁾ A_{2ω} A_ω* e^{−iΔk z}
dA_{2ω}/dz = i(4ω²/2k_{2ω}c²) χ⁽²⁾ A_ω² e^{+iΔk z}
```

with Δk = k_{2ω} − 2k_ω. These are the fundamental coupled-wave equations
(Boyd §2). The sine-squared solution η = η₀ sinc²(Δk L/2) emerges from
integrating them.

**Quasi-phase matching (QPM)**: When birefringent phase matching is impossible
(e.g., isotropic materials or desired nonlinear coefficient d_eff too small),
periodically POLE the crystal (flip the sign of χ⁽²⁾ every L_coh = π/Δk).
This creates a grating k_G = 2π/Λ such that Δk_QPM = Δk − k_G = 0, allowing
SHG even in non-birefringent materials like periodically-poled LiNbO₃ (PPLN).

**Stimulated Raman/Brillouin scattering**: χ⁽³⁾-mediated inelastic scattering
where the frequency shift is set by a material resonance:
- Raman: optical phonons (Δν ∼ 10 THz in silica); used for amplifiers and
  frequency combs.
- Brillouin: acoustic phonons (Δν ∼ 10 GHz, gain bandwidth ∼ 10-100 MHz);
  limits power in fibers (SBS threshold ∼ mW for narrow-linewidth lasers).
Both follow coupled intensity equations: dI_s/dz = g_R I_p I_s (Raman gain).

**Self-steepening and soliton formation**: The intensity-dependent group
velocity n(I) = n₀ + n₂I creates a nonlinear term ∝ ∂(I E)/∂t in the
propagation equation. In the anomalous dispersion regime (β₂ < 0), this
balances dispersion → solitons. This is the bridge to `reasoning.optics.pulse_propagation_nlse`.

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

**Two-photon absorption (TPA)**: α = α₀ + β I where β ∝ Im[χ⁽³⁾]. A photon
pair is simultaneously absorbed to excite a transition of energy 2ℏω. TPA
is the dominant loss mechanism in semiconductors at high intensity; it sets
a practical limit for all-optical switching. Free-carrier absorption (FCA)
from TPA-generated carriers further increases loss.

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

## Edge Cases

- **Phase matching fails (Δk ≠ 0)**: Conversion oscillates with period
  L_coh = π/Δk. When birefringent phase matching is impossible (e.g.,
  cubic crystals, or the desired χ⁽²⁾ component has zero d_eff), switch to
  quasi-phase matching (QPM) with periodically-poled crystals — the domain
  inversion grating compensates Δk, enabling any χ⁽²⁾ component in any
  material (Fejer, IEEE JQE 1992).
- **Walk-off (spatial and temporal)**: Birefringent phase matching separates
  ordinary and extraordinary beams spatially (Poynting vector walk-off,
  angle ρ ∼ 1°-5°). Temporal walk-off (group-velocity mismatch, GVM) limits
  interaction length for short pulses. Solution: non-critical phase matching
  (θ=90°) eliminates spatial walk-off; chirped QPM gratings compensate GVM.
- **Depletion of pump — small-signal approximation breaks down**: The SVEA
  analytic solutions assume undepleted pump (A_ω ≈ const). When η > ~10%,
  pump depletion is significant — use numerical integration of the full
  coupled-wave equations or Jacobi elliptic function solutions (Armstrong
  et al., Phys. Rev. 1962).
- **Thermal lensing / damage**: At high average power, residual absorption
  heats the crystal → thermal lens (dn/dT) distorts the beam, reducing
  efficiency. When thermal lens power > 1/f_beam, switch to cryogenic
  cooling, thin-disk geometry, or cavity-dumped operation.

## Cross-References

- Avetissian §2-3 (nonlinear Compton, induced Cherenkov)
- Born & Wolf §12 (nonlinear optics basics)
- landau-graph: knowledge.continuous.dielectric_dispersion (linear regime)
- landau-graph: reasoning.constitutive_relation_from_symmetry (χ⁽ⁿ⁾ tensor symmetry)
- optics: reasoning.optics.pulse_propagation_nlse (γ from χ⁽³⁾ → Kerr coefficient
  n₂ feeds NLSE soliton formation; bidirectional: NLSE consumes this parent)
