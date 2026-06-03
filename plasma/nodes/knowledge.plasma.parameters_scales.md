---
skill_id: knowledge.plasma.parameters_scales
type: knowledge
summary_50t: >
  λ_D=√(ε₀T_e/n₀e²), N_D=n₀λ_D³≫1, ω_p=√(n₀e²/ε₀m), ω_c=eB₀/m,
  r_L=v_⊥/ω_c, β=2μ₀p/B₀², lnΛ≈10-20. Collision frequency ν_ei.
  Magnetization: ω_c τ > 1. Saha equation for ionization balance.
trigger: computing basic plasma parameters, determining regime
reasoning_role: plasma_parameters
parent: reasoning.plasma.dispersion_relation_method
retrieval_cost: 1
---

# knowledge.plasma.parameters_scales

**Debye shielding**: λ_D = √(ε₀T_e/n₀e²) ≈ 743√(T_e[eV]/n₀[cm⁻³]) cm.
N_D = (4π/3)n₀λ_D³ ≫ 1 (plasma condition: collective behavior).

**Plasma frequency**: ω_p = √(n₀e²/ε₀m_e) ≈ 5.64×10⁴√n₀[cm⁻³] rad/s.
f_p = ω_p/2π ≈ 8980√n₀[cm⁻³] Hz.

**Cyclotron**: ω_ce = eB₀/m_e ≈ 1.76×10¹¹ B₀[T] rad/s.
f_ce ≈ 28 B₀[T] GHz. Larmor radius: r_L = v_⊥/ω_c = m v_⊥/eB₀.

**Collisions**: ν_ei ≈ 2.9×10⁻¹² n₀[cm⁻³] lnΛ T_e[eV]^{−3/2} s⁻¹.
Coulomb logarithm: lnΛ ≈ 10 (dense, cold) to 20 (dilute, hot).

**Beta**: β = 2μ₀ n T/B₀² ≈ 4.0×10⁻²⁵ n[cm⁻³] T[eV] / B₀[T]².

**Critical density** (laser): n_c[cm⁻³] = 1.1×10²¹ / λ_μm².
**Collisionless**: ω ≫ ν_ei. **Magnetized**: ω_c τ ≫ 1.

- Chen §1-3
