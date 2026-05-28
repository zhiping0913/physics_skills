---
skill_id: knowledge.condensed.green_function
type: knowledge
summary_50t: >
  G_αβ(x,x') = −i⟨T ψ_α(x)ψ†_β(x')⟩. Spectral function A(ω,p).
  Dyson: G = G₀ + G₀ΣG. Σ = self-energy. Quasiparticle: Z/(ω−ε+iγ).
  Wick theorem → diagram technique.
trigger:
  - computing propagator for interacting system
  - extracting spectrum from Green's function
  - Feynman diagram expansion
reasoning_role: many_body_propagator
parent: reasoning.green_function_method
retrieval_cost: 1
---

# knowledge.condensed.green_function

**Definition**: G(x,x') = −i⟨T ψ(x)ψ†(x')⟩ (T=0), thermal at T>0.
For homogeneous system: G(ω,p) = Fourier transform.

**Non-interacting** (T=0): G₀(ω,p) = 1/(ω−ε_p+iδ sgn(p−p_F))
where ε_p = p²/2m−μ.

**Spectral representation**: G(ω,p) = ∫ A(ω',p)/(ω−ω'+i0) dω'/2π.
A(ω,p) = −(1/π) Im G_R(ω,p) ≥ 0.

**Dyson equation**: G = G₀ + G₀ΣG → G⁻¹ = G₀⁻¹ − Σ.
Σ(ω,p) complex: Re Σ → energy shift, Im Σ → damping ∝ inverse lifetime.

**Fermi liquid**: G ≈ Z/(ω−v_F(p−p_F)+iγ), γ ∝ (p−p_F)²+T².

**Wick theorem**: ⟨T ψ₁ψ₂...ψ_n⟩ = Σ (contractions). Each contraction = G₀.
→ Diagram technique: vertices (interaction) + lines (G₀).

- Landau Vol.9 §7-21
