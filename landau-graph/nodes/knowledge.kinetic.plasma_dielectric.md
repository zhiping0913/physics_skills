---
skill_id: knowledge.kinetic.plasma_dielectric
type: knowledge
summary_50t: >
  ε_l(k,ω). Langmuir: ω²=ω_p²+3k²v_T². Debye: a_D=√(T/4πne²).
  Ion-acoustic: ω=kc_s. Two-temperature plasma (T_e ≠ T_i).
  Spatial dispersion removes ω=0 pole of conducting medium.
trigger:
  - plasma wave dispersion
  - Debye screening
  - plasma dielectric function
reasoning_role: plasma_linear_response
parent: reasoning.plasma_dielectric_response
retrieval_cost: 1
---

# knowledge.kinetic.plasma_dielectric

**Plasma frequency**: ω_p = √(4πne²/m). ω_p/2π ≈ 9√n  Hz (n in cm⁻³).

**Debye length**: a_D = √(T/4πne²). Screened potential: φ ∝ e^{−r/a_D}/r.
A plasma is "collisionless" when N_D = n(4π/3)a_D³ ≫ 1 (many particles in Debye sphere).

**Langmuir waves**: ε_l(k,ω) = 0 → ω² = ω_p² + 3k²v_T² (Bohm-Gross).
Phase velocity v_ph = ω/k > v_T for weak damping.

**Ion-acoustic waves**: ω = kc_s, c_s = √(ZT_e/M) for T_e ≫ T_i.
Requires T_e ≫ T_i for weak damping — otherwise strong ion Landau damping.

**Static screening**: ε_l(k,0) = 1 + (ka_D)⁻².
Test charge: φ_k = 4πq/(k²ε_l(k,0)) → φ(r) = q e^{−r/a_D}/r.

- Landau Vol.10 §29-33
