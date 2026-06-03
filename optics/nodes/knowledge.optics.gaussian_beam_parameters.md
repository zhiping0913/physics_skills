---
skill_id: knowledge.optics.gaussian_beam_parameters
type: knowledge
summary_50t: >
  w(z)=w₀√(1+(z/z_R)²), R(z)=z+z_R²/z, z_R=πw₀²/λ. ABCD: free space[1 L;0 1],
  lens[1 0;−1/f 1], mirror[1 0;−2/R 1]. Stability 0<g₁g₂<1, g=1−L/R.
  M²≥1, B=P/(λ²M²)². Matching: w₀₂/w₀₁=√(f²/((z₁−f)²+z_R₁²))·z_R₁.
trigger: computing beam size, wavefront, resonator mode, mode matching
reasoning_role: beam_parameters
parent: reasoning.optics.gaussian_beam_optics
retrieval_cost: 1
---

# knowledge.optics.gaussian_beam_parameters

**Beam propagation**: w(z)=w₀√(1+(z/z_R)²), R(z)=z+z_R²/z, ψ(z)=arctan(z/z_R).
Rayleigh range z_R=πw₀²/λ. Far-field divergence θ=λ/(πw₀) (half-angle).

**ABCD matrices**: Free space L: [1 L;0 1]. Thin lens f: [1 0;−1/f 1].
Mirror R: [1 0;−2/R 1]. Dielectric interface (n₁→n₂): [1 0;0 n₁/n₂].
Gaussian duct (graded-index, n=n₀−½n₂r²): cos/sin matrix, period 2π/√(n₂/n₀).

**Resonator**: g₁=1−L/R₁, g₂=1−L/R₂. Stable: 0<g₁g₂<1.
Waist: w₀²=(λL/π)√(g₁g₂(1−g₁g₂))/(g₁+g₂−2g₁g₂) (symmetric).

**M²**: M²=πw₀θ/λ≥1. Real beam: w(z)=w₀√(1+M⁴(z−z₀)²/z_R²).
Brightness B=P/(λ²M_x²M_y²) ≈ invariant in lossless passive systems.

**Mode matching**: single lens f at distance d₁ from beam 1. Required
d₂ = f ± (w₀₂/w₀₁)√(f²−f₀²) where f₀=πw₀₁w₀₂/λ.

- Siegman §16-21, Marcuse §2-4
