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

## Millimeter-Wave Propagation and Frequency Scaling

**Atmospheric attenuation** (ITU-R P.676): molecular absorption creates
transmission windows. Key features:
- O₂ absorption peak at 60 GHz (∼15 dB/km at sea level) — the dominant
  mm-wave loss mechanism
- H₂O absorption peaks at 22 GHz and 183 GHz
- **Windows**: 35 GHz (Ka-band), 94 GHz (W-band), 220 GHz, 340 GHz
- 60-GHz paradox: high atmospheric loss → natural isolation between
  neighboring links → ideal for short-range unlicensed communication
  (5G NR bands n257/n258/n260/n261).

**Frequency-scaling laws** (fixed physical aperture A):
```
G ∝ f²          (gain ∝ frequency squared — from G = 4πA_eff/λ²)
HPBW ∝ 1/f      (beamwidth narrows with frequency)
```
These drive the push to higher frequencies: for the same antenna size,
doubling the frequency quadruples the gain and halves the beamwidth.

**Rain attenuation** (ITU-R P.838): specific attenuation ∝ k R^α where R is
rain rate (mm/hr). k and α depend on frequency and polarization. At 60 GHz,
moderate rain (10 mm/hr) adds ∼10-20 dB/km — the dominant weather loss above
20 GHz.

**Free-space path loss**: L_fs = (4πR/λ)². At 60 GHz and R = 100 m,
L_fs ≈ 108 dB — demands high-gain antennas even for short links.

- Jackson §9.2-9.8, Griffiths §11.1-11.3
- ITU-R P.676 (atmospheric attenuation), ITU-R P.838 (rain attenuation)
