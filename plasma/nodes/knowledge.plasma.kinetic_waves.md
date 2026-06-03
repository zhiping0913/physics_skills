---
skill_id: knowledge.plasma.kinetic_waves
type: knowledge
summary_50t: >
  Landau γ=(π/2)(ω_p²/k²)∂f₀/∂v. Ion acoustic ω²=k²c_s²/(1+k²λ_D²).
  Bernstein: ω=nω_c, undamped. Drift: ω*=k_yT_e/eB₀n₀ dn₀/dx.
  Bohm-Gross: ω²=ω_p²+3k²v_th². Kinetic Alfvén: k⊥ρ_i∼1.
trigger: computing hot-plasma wave dispersion, kinetic damping rates
reasoning_role: kinetic_waves
parent: reasoning.plasma.wave_particle_resonance
retrieval_cost: 1
---

# knowledge.plasma.kinetic_waves

**Landau damping**: γ_L = (π/2)(ω_p²/k²)∂f₀/∂v|_{v=ω/k}. Phase mixing of
resonant particles → exponential decay. Reversible in collisionless plasma
(plasma echo).

**Ion acoustic**: ω² = k²c_s²/(1+k²λ_D²), c_s=√(ZT_e/m_i). Requires T_e≫T_i
to overcome ion Landau damping. Strongly damped for T_e∼T_i.

**Langmuir (Bohm-Gross)**: ω² = ω_p² + 3k²v_th². Electron plasma wave.
ω→ω_p at long wavelength.

**Bernstein** (k⊥B₀): ω=nω_c, pure electrostatic, undamped when k_∥=0.
Propagates in bands between cyclotron harmonics.

**Drift wave**: ω*=k_y v_de, v_de=−(T_e/eB₀ n₀)dn₀/dx. Universal instability
in confined plasma. Drives tokamak turbulence.

**Kinetic Alfvén** (k⊥ρ_i∼1): E_∥≠0 from finite Larmor radius. Important
for auroral electron acceleration, tokamak edge.

- Stix §8-9, Chen §7, Ginzburg §6-7
