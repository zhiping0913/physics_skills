---
skill_id: knowledge.em.fresnel_reflection_transmission
type: knowledge
summary_50t: >
  r_s,r_p,t_s,t_p formulas. Brewster tanθ_B=n₂/n₁ (p-pol only). TIR θ>θ_c=arcsin(n₂/n₁),
  evanescent: E∝e^{−κz}, Goos-Hänchen Δ∼λ. Metal ñ=n+iκ→complex r. Power R=|r|².
  Thin film: r=(r₁₂+r₂₃e^{2iβ})/(1+r₁₂r₂₃e^{2iβ}), β=kn₂d cosθ₂.
trigger: computing reflection/transmission at dielectric or metal interfaces
reasoning_role: fresnel_data
parent: reasoning.em.fresnel_interface_reflection_refraction
retrieval_cost: 1
---

# knowledge.em.fresnel_reflection_transmission

**s-pol**: r_s=(n₁cosθ_i−n₂cosθ_t)/(n₁cosθ_i+n₂cosθ_t), t_s=2n₁cosθ_i/(...).
**p-pol**: r_p=(n₂cosθ_i−n₁cosθ_t)/(n₂cosθ_i+n₁cosθ_t), t_p=2n₁cosθ_i/(...).
**Power**: R=|r|², T=(n₂cosθ_t/n₁cosθ_i)|t|². R+T=1 (lossless dielectric).

**Brewster**: r_p=0 at tanθ_B=n₂/n₁. Reflected light pure s-pol. Laser Brewster
windows eliminate p-pol reflection loss. **TIR**: θ_c=arcsin(n₂/n₁). n₁>n₂ required.
Evanescent field: E_t∝exp(−κz), κ=k₀√(n₁²sin²θ_i−n₂²). Penetration depth d_p=1/κ.
Frustrated TIR: second prism at d<d_p→tunneling→beam splitter.

**Metals** (ñ=n+iκ): |r_s|²,|r_p|²→1 for thick. R_min at pseudo-Brewster.
**Thin film**: r=(r₁₂+r₂₃e^{2iβ})/(1+r₁₂r₂₃e^{2iβ}), β=2πn₂d cosθ₂/λ.
Antireflection: n_coat=√(n₁n₃), d=λ/4→R=0 at design λ.

- Jackson §7.3, Born & Wolf §1.5, Griffiths §9.3
