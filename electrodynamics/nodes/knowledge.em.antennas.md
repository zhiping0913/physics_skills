---
skill_id: knowledge.em.antennas
type: knowledge
summary_50t: >
  Hertzian dipole: R_rad=80π²(dl/λ)², pattern ∝ sin²θ. Half-wave: Z_in≈73Ω.
  Arrays: total pattern=(element)×(array factor). Gain G=4πA_eff/λ².
  Aperture: uniform distribution → first sidelobe −13.3dB.
trigger:
  - computing antenna radiation resistance, pattern, gain, beamwidth
reasoning_role: antenna_knowledge
parent: reasoning.em.antenna_radiation_pattern
retrieval_cost: 1
---

# knowledge.em.antennas

**Hertzian dipole** (dl ≪ λ, I₀):
R_rad = 80π²(dl/λ)², P = ½I₀²R_rad
dP/dΩ = (η/8)(I₀ dl/λ)² sin²θ
Directivity: D_max = 1.5 (1.76 dBi)

**Half-wave dipole** (L=λ/2, I(z)=I₀cos(πz/L)):
Z_in ≈ 73 + j42.5 Ω (resonant when slightly shortened)
dP/dΩ = (ηI₀²/8π²)[cos(π/2 cos θ)/sin θ]²
D_max ≈ 1.64 (2.15 dBi), HPBW ≈ 78°

**Arrays** (N isotropic elements, spacing d, phase δ):
Array factor: AF = |Σ_{n=0}^{N−1} e^{jn(kd cos θ+δ)}| = |sin(Nψ/2)/sin(ψ/2)|
Grating lobe condition: kd(1+cos θ_max) = 2πn → avoid with d<λ/2.
Phased array: varying δ steers beam without mechanical rotation.

**Aperture antennas**:
Gain: G = 4πA_eff/λ² (A_eff ≤ A_physical, efficiency η_a = A_eff/A).
Uniform rectangular aperture (a×b): HPBW ≈ 0.886λ/a, first sidelobe −13.3 dB.
Circular aperture (radius a): HPBW ≈ 1.02λ/(2a), first sidelobe −17.6 dB.

**Friis transmission**: P_r/P_t = G_t G_r (λ/4πR)².
**Radar range equation**: P_r = P_t G_t G_r λ²σ/[(4π)³R⁴].

- Jackson §9.2-9.8, Griffiths §11.1-11.3
