---
skill_id: knowledge.plasma.cold_magnetized_waves
type: knowledge
summary_50t: >
  CMA diagram: (ω_p²/ω², ω_c/ω) space → wave topology. R-wave (whistler,
  ω_ce resonance), L-wave (ω_ci), O-mode (P=0 cutoff), X-mode (RL/S,
  UH/LH resonances). Whistler: ω∝k² at low ω. Faraday rotation: Δψ∝∫n_eB_∥dl.
trigger: identifying cold-plasma wave modes, computing refractive index
reasoning_role: cma_diagram
parent: reasoning.plasma.dielectric_tensor_magnetized
retrieval_cost: 1
---

# knowledge.plasma.cold_magnetized_waves

**Stix parameters** (cold, collisionless):
R,L = 1 − Σ ω_pα²/[ω(ω±ω_cα)], S=½(R+L), D=½(R−L), P=1−Σ ω_pα²/ω².

**∥ propagation (θ=0)**:
R-wave: N²=R, RH circ. Whistler at ω_ci≪ω≪ω_ce: N²≈ω_pe²/ωω_ce → ω∝k².
L-wave: N²=L, LH circ. Ion cyclotron resonance at ω_ci.

**⊥ propagation (θ=π/2)**:
O-mode: N²=P, E∥B₀, cutoff at ω=ω_p.
X-mode: N²=RL/S, E⊥B₀, cutoffs R=0,L=0; resonances S=0 (UH: ω²=ω_p²+ω_ce²; LH: ω_LH²≈ω_ci ω_ce).

**Faraday rotation**: Δψ = (e³λ²/8π²ε₀m_e²c³)∫n_e B_∥ dl.
Diagnostics: measure Δψ → ∫n_e B_∥.

**Goos-Hänchen**: negative at S→0 resonance → reflects away from resonance layer.

- Stix §1-4, Ginzburg §3-5, Chen §4
