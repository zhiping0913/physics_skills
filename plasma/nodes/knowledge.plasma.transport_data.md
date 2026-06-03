---
skill_id: knowledge.plasma.transport_data
type: knowledge
summary_50t: >
  Braginskii η_∥=5.2×10⁻⁵ZlnΛ/T_e^{3/2} Ω·m. D_⊥=η_∥nT/B₀². Neo: banana
  ν*=νqR/v_thε^{3/2}, χ∝q²ε^{−3/2}χ_cl. Bootstrap j_BS∼√ε dp/dr/B_θ.
  Anomalous: D_turb∼γ/k_⊥². Scaling τ_E∝I_p^α P^{−β} (IPB98).
trigger: computing plasma transport coefficients, confinement scaling
reasoning_role: transport_data
parent: reasoning.plasma.transport_coefficients
retrieval_cost: 1
---

# knowledge.plasma.transport_data

**Classical** (Braginskii 1965): η_∥=5.2×10⁻⁵ Z lnΛ/T_e[eV]^{3/2} Ω·m.
χ_e∥=3.2 n_e T_e/(m_e ν_ei). χ_e⊥=χ_e∥/(1+ω_ce²τ_ei²). χ_i⊥ similarly.
D_⟂=η_∥nT/B₀². Off-diagonal: thermo-electric (E from ∇T), Nernst, Ettingshausen.

**Neoclassical**: ν*=νqR/(v_th ε^{3/2}) [ε=r/R]. Banana (ν*≪1): trapped particles,
χ_ban≈q²ε^{−3/2}χ_cl. Plateau (ν*∼1): χ∝T/(B₀R)ρ_i²ν. Pfirsch-Schlüter (ν*≫1):
χ_PS≈(1+1.6q²)χ_cl. Bootstrap: j_BS=−(ε^{1/2}/B_θ)(dp/dr)F(ν*). F→1 in banana.

**Anomalous**: mixing-length D_turb∼γ_max/k_⊥² from dominant microinstability.
ITG (η_i=dlnT_i/dlnn_i>1): χ_i∼ρ_s²c_s/L_T. TEM: χ_e∼ similar. ETG: χ_e small
but critical for stiffness. Energy confinement: τ_E=W/P_loss. IPB98(y,2):
τ_E∝I_p^{0.93}B₀^{0.15}n^{0.41}P^{−0.69}R^{1.97}ε^{0.58}κ^{0.78}.

- Chen §5, Wesson §3, Handbook Pt.1
