---
skill_id: knowledge.em.nonlinear_optics
type: knowledge
summary_50t: >
  SHG: d_eff for common crystals (KDP, BBO, LiNbO₃). Phase matching:
  Type I (o+o→e), Type II (o+e→e). OPO: ω_p→ω_s+ω_i, threshold ∝ 1/Q².
  Self-focusing: P_cr≈λ²/8πn₀n₂. Soliton: balance SPM + anomalous GVD.
trigger:
  - designing frequency conversion, parametric amplifiers, mode-locked lasers
reasoning_role: nonlinear_knowledge
parent: reasoning.em.nonlinear_optical_response
retrieval_cost: 1
---

# knowledge.em.nonlinear_optics

**SHG crystals**: KDP (d₃₆≈0.39 pm/V), BBO (d₂₂≈2.2 pm/V), LiNbO₃ (d₃₃≈27 pm/V).
Periodically-poled LiNbO₃ (PPLN): quasi-phase matching (QPM) → d_eff≈(2/π)d₃₃.
Conversion: η = tanh²(√(η₀)L) → for strong pump, η→100%.

**Phase matching types** (uniaxial, n_e < n_o):
Type I: o+o→e. n_o(ω) = n_e(2ω,θ_m). θ_m from 1/n_e²(θ)=cos²θ/n_o²+sin²θ/n_e².
Type II: o+e→e. ½[n_o(ω)+n_e(ω,θ_m)] = n_e(2ω,θ_m).
Temperature tuning: n(T) varies → phase match by changing crystal temperature.

**Optical parametric oscillator (OPO)**: χ⁽²⁾ process, pump ω_p→signal ω_s+idler ω_i.
Threshold: P_th ∝ (1−R)/(d_eff²L²Q_p Q_s). Doubly resonant (DRO): lower threshold,
tunable via phase matching. Singly resonant (SRO): simpler, more stable.

**Kerr lens mode-locking (KLM)**: n₂>0→self-focusing→higher gain for pulsed mode.
Produces femtosecond pulses (Ti:Sapphire: Δt∼5fs, Δλ∼200nm, P_peak∼MW).

**Soliton** (optical fiber): balance GVD (β₂<0, anomalous) + SPM (n₂>0).
Fundamental soliton: P₀ = |β₂|/(γT₀²). Shape: sech(t/T₀). Propagation stable.

**Self-phase modulation (SPM)**: φ_NL = n₂k₀I·L_eff. Frequency chirp:
Δω(t)=−∂φ_NL/∂t. Spectral broadening: Δω_max ∝ (n₂ω₀/c)(I₀ L_eff/T₀).
Combined with GVD → pulse compression or soliton formation.

- Avetissian §2-3; Boyd, Nonlinear Optics (standard reference)
