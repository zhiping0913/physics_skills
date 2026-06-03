---
skill_id: knowledge.em.optics_of_metals
type: knowledge
summary_50t: >
  Drude: ε(ω)=1−ω_p²/(ω²+iγω). Skin δ=√(2/μ₀σω). ñ=n+iκ: R=|(ñ−1)/(ñ+1)|².
  Noble metals: Ag ε'<0 for λ>320nm (interband at 3.8eV), Au at 2.4eV.
  Plasma frequency: ω_p=√(ne²/ε₀m). R→1 for ω<ω_p. Hagen-Rubens: R≈1−2√(2ε₀ω/σ).
trigger: optical properties of metals, skin effect, plasmonic materials
reasoning_role: metal_optics
parent: reasoning.em.fresnel_interface_reflection_refraction
retrieval_cost: 1
---

# knowledge.em.optics_of_metals

**Drude model** (free electrons): ε(ω)=1−ω_p²/(ω²+iγω). ω_p=√(ne²/ε₀m_e).
Ag: ω_p≈9eV (λ_p≈138nm), ω_p≈1.4×10¹⁶ rad/s. τ=1/γ (relaxation time).
DC conductivity: σ₀=ε₀ω_p²τ. Skin depth: δ=√(2/μ₀σω) (classical, ωτ≪1).
Anomalous skin effect (ωτ≫1, δ<l_mfp): δ∝ω^{−1/3}.

**Complex refractive index**: ñ=n+iκ. ε₁=n²−κ², ε₂=2nκ. Reflectivity at
normal incidence: R=|(ñ−1)/(ñ+1)|²=[(n−1)²+κ²]/[(n+1)²+κ²].
For κ≫n (good conductor): R≈1−2/(κ+1)≈1−2/κ.

**Interband transitions**: Ag 3.8eV (≈326nm), Au 2.4eV (≈517nm), Cu 2.1eV (≈590nm).
Below interband edge: ε₁<0 (Drude-like). At interband: ε₂ peaks, ε₁ crosses zero.
Surface plasmon condition: ε₁(ω)=−ε_d (interface with dielectric ε_d).

**Hagen-Rubens** (far IR, ω≪1/τ): R≈1−2√(2ε₀ω/σ₀). Measured σ₀→R(ω).

- Born & Wolf §15, Jackson §7.5
