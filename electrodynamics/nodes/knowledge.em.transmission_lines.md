---
skill_id: knowledge.em.transmission_lines
type: knowledge
summary_50t: >
  TEM: Z₀=√(L/C). Coax: Z₀=(η₀/2π)ln(b/a)≈60ln(b/a)Ω. Γ=(Z_L−Z₀)/(Z_L+Z₀).
  VSWR=(1+|Γ|)/(1−|Γ|). λ/4 transformer: Z₁=√(Z₀ Z_L). Smith chart: Z→Γ plane.
trigger: impedance matching, power transfer in TEM transmission lines
reasoning_role: transmission_lines
parent: reasoning.em.waveguide_mode_decomposition
retrieval_cost: 1
---

# knowledge.em.transmission_lines

**TEM mode** (Ez=Hz=0): V,I satisfy telegrapher's equations. Propagation
constant γ=α+iβ=√((R+iωL)(G+iωC)). Lossless: β=ω√(LC), v_p=1/√(LC)=c/n.
Characteristic impedance Z₀=√(L/C). Coaxial: L=(μ/2π)ln(b/a), C=2πε/ln(b/a)
→ Z₀=(1/2π)√(μ/ε)ln(b/a)≈(60/√ε_r)ln(b/a) Ω. Microstrip: Z₀≈(87/√(ε_r+1.41))ln(5.98h/(0.8w+t)).

**Reflection**: Γ=(Z_L−Z₀)/(Z_L+Z₀). Matched Z_L=Z₀→Γ=0. Short Z_L=0→Γ=−1.
Open Z_L=∞→Γ=+1. VSWR=(1+|Γ|)/(1−|Γ|). Return loss RL=−20log₁₀|Γ| dB.

**Impedance matching**: λ/4 transformer: Z₁²=Z₀ Z_L (single frequency).
Stub tuning: shunt open/short stub at distance d from load. Smith chart:
normalized impedance z=r+jx mapped to Γ-plane → graphical design.

**Power**: P_avg=(|V₀⁺|²/2Z₀)(1−|Γ|²). Maximum available power (conjugate
match: Z_L=Z₀*). Attenuation: α=α_c+α_d (conductor + dielectric loss).

- Jackson §8.1
