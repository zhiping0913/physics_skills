---
skill_id: knowledge.condensed.diagram_technique
type: knowledge
summary_50t: >
  Wick theorem → Feynman diagrams. Each diagram = mathematical expression.
  Dyson equation sums infinite series. Self-energy Σ from 1PI diagrams.
  Vertex function Γ from 3-point diagrams. Universal language of QFT.
trigger:
  - perturbative expansion of Green's functions
  - computing self-energy, vertex corrections
  - systematic approximation schemes (RPA, ladder, etc.)
reasoning_role: perturbative_expansion
parent: reasoning.green_function_method
retrieval_cost: 1
---

# knowledge.condensed.diagram_technique

**Wick's theorem**: Time-ordered product = sum of all possible contractions.
Each contraction ⟨T ψ ψ†⟩ = iG₀ → wavy line.

**Feynman rules** (fermions with interaction V):
- Solid line → G₀(ω,p) = 1/(ω−ε_p+sgn(p−p_F)i0)
- Dashed line → V(q) (interaction potential)
- Vertex → factor of −i. Momentum/energy conserved at each vertex.
- Closed loop → −1 factor (fermions). Integrate over all internal variables.

**Dyson equation**: G = G₀ + G₀ΣG  →  G = 1/(G₀⁻¹ − Σ).
Σ = sum of all one-particle-irreducible (1PI) diagrams.

**Key diagrams**:
- Hartree-Fock: Σ^(1) = direct + exchange
- RPA (Random Phase Approximation): sum of bubble diagrams → screened interaction
- Ladder: sum of repeated scattering → vertex function

**Vertex function Γ**: 3-point function = scattering amplitude of quasiparticles.
Connected to Landau f-function: Γ^ω (p₁,p₂) = f(p₁,p₂) in ω→0, q→0 limit.

**Temperature technique** (§36-38): t → −iτ, ω → iω_n = iπT(2n+1) for fermions.
Matsubara frequencies. Sums over discrete frequencies replace integrals.

- Landau Vol.9 §13-14, §38
