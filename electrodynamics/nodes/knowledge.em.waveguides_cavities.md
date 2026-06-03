---
skill_id: knowledge.em.waveguides_cavities
type: knowledge
summary_50t: >
  Rectangular: TE_mn, TM_mn with k_⊥²=(mπ/a)²+(nπ/b)², cutoff f_c=c k_⊥/2π.
  Circular: TE/TM with Bessel zeros. Coax: TEM, no cutoff, Z₀=(1/2π)√(μ/ε)ln(b/a).
  Cavities: resonant modes with Q = ω₀·(stored energy)/(power loss).
trigger:
  - designing microwave/optical waveguides or resonant cavities
  - need mode structure, cutoff, impedance, Q factor
reasoning_role: waveguide_knowledge
parent: reasoning.em.waveguide_mode_decomposition
retrieval_cost: 1
---

# knowledge.em.waveguides_cavities

## Rectangular Waveguide (a × b, a > b)

TE_mn modes (E_z=0): H_z = H₀ cos(mπx/a) cos(nπy/b)
TM_mn modes (H_z=0): E_z = E₀ sin(mπx/a) sin(nπy/b)
Cutoff: f_c(mn) = (c/2)√[(m/a)²+(n/b)²]
Dominant mode: TE₁₀ (lowest cutoff, f_c=c/2a)
Single-mode band: c/2a < f < c/a
Power: P_TE₁₀ = (ab/4Z_TE) E₀²,  Z_TE = η/√[1−(f_c/f)²]

## Circular Waveguide (radius R)

TE_nm: k_⊥ = x'_nm/R  (J'_n(x'_nm)=0). TE₁₁: x'₁₁≈1.841.
TM_nm: k_⊥ = x_nm/R   (J_n(x_nm)=0).  TM₀₁: x₀₁≈2.405.
Lowest loss mode: TE₀₁ (H_φ only, wall currents circumferential → low loss).

## Coaxial Cable

TEM mode: E = (V₀/ρ ln(b/a)) ρ̂, H = (I₀/2πρ) φ̂.
Characteristic impedance: Z₀ = (η/2π) ln(b/a), η=√(μ/ε)≈377Ω.
No cutoff (propagates DC to optical). Attenuation minimum at b/a≈3.6.

## Resonant Cavities

Rectangular cavity (a×b×d): resonant at f_lmn = (c/2)√[(l/a)²+(m/b)²+(n/d)²].
Quality factor: Q = ω₀ U/P_loss.
TE₁₀₁ mode: Q ≈ (η/2R_s)·(volume/surface_area) ∼ 10⁴ for copper at 10 GHz.

## Dielectric Waveguides (Optical Fiber)

Step-index fiber: core radius a, n_core > n_clad.
Single-mode condition: V = (2πa/λ)√(n_core²−n_clad²) < 2.405.
LP₀₁ mode: near-Gaussian profile, minimal dispersion near λ≈1.55μm.

- Jackson §8.1-8.7
