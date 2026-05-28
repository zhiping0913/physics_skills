---
skill_id: reasoning.plasma_dielectric_response
type: reasoning
summary_50t: >
  ε_l(k,ω) = 1 − (4πe²/k²)∫(k·∂f/∂p)/(kv−ω−i0) d³p.
  Complex ε → reactive (dispersion) + dissipative (Landau damping).
  Spatial dispersion (k-dependence) is essential — eliminates ω=0 pole.
trigger:
  - dielectric response of collisionless plasma
  - plasma wave dispersion relation
  - screening, Debye shielding
reasoning_role: linear_response
parent: reasoning.kinetic_equation_closure
children:
  - knowledge.kinetic.plasma_dielectric
retrieval_cost: 1
---

# reasoning.plasma_dielectric_response — Kinetic Theory → ε(k,ω)

## Core Picture

In a plasma, the dielectric function ε(k,ω) is computed directly from the
Vlasov equation — no phenomenological parameters. The result depends on k
(spatial dispersion) and has an imaginary part (Landau damping).

This is fundamentally different from ordinary dielectrics where ε is
introduced phenomenologically.

## Key Results

**Long-wavelength limit** (k→0): ε(ω) = 1 − ω_p²/ω².
Langmuir waves: ω² = ω_p² + 3k²v_T² (Bohm-Gross dispersion).

**Debye screening**: static (ω=0) limit → ε_l(k,0) = 1 + 1/(ka_D)².
Screened Coulomb potential: φ(r) ∝ e^{−r/a_D}/r, a_D = √(T/4πne²).

**Landau damping rate** (Maxwellian, ω/kv_T ≫ 1):
γ = −√(π/8) ω_p (ω_p/kv_T)³ exp(−ω_p²/2k²v_T²).

**Ion-acoustic waves**: ω = kc_s, c_s = √(ZT_e/M) for T_e ≫ T_i.
Damping: weak when T_e ≫ T_i, strong when T_e ≈ T_i.

## Two-Component Plasma

ε_l − 1 = contribution from electrons + contribution from ions.
Each with its own temperature T_e, T_i and Debye length a_e, a_i.
Two-temperature plasma arises naturally because τ_ei ≫ τ_ee.

## Edge Cases

- **ω < kv_T**: strong Landau damping, wave concept fails
- **Degenerate plasma**: f_0 = Fermi-Dirac → different ε
- **Magnetized**: ε becomes a tensor with cyclotron resonances

## Cross-References
- Landau Vol.10 §29-33
- Landau Vol.8 §62 (general properties of ε(ω))
- **Landau damping IS spatial dispersion**: Without k-dependence, Im ε = 0
  and there is no collisionless dissipation. The Landau damping mechanism
  is the dissipative manifestation of spatial dispersion in a plasma.
  See reasoning.spatial_dispersion (Vol.8 §103).
