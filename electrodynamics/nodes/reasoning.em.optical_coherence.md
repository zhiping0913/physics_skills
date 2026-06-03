---
skill_id: reasoning.em.optical_coherence
type: reasoning
summary_50t: >
  Real sources are partially coherent: mutual coherence Γ(r₁,r₂,τ)=⟨E(r₁,t+τ)E*(r₂,t)⟩
  governs interference visibility. van Cittert-Zernike: spatial coherence ↔
  source Fourier transform. Wiener-Khinchin: power spectrum ↔ autocorrelation.
trigger:
  - interference with real (non-laser) light sources
  - computing fringe visibility in interferometers
  - stellar interferometry, coherence tomography
reasoning_role: coherence_theory
parent: reasoning.fluctuation_dissipation_quantum
retrieval_cost: 1
references:
  - landau-graph: reasoning.fluctuation_dissipation_quantum
---

# reasoning.em.optical_coherence — Statistical Fields → Interference Limits

## Core Picture

Perfectly monochromatic plane waves produce perfect interference. Real light
sources (thermal, LED, even lasers) have finite bandwidth and spatial extent
→ only PARTIALLY coherent. Coherence theory quantifies the degree to which
a field can produce interference.

## Key Quantities (Born & Wolf §10)

**Mutual coherence function** (spatio-temporal):
Γ(r₁, r₂, τ) = ⟨E(r₁, t+τ) E*(r₂, t)⟩

**Complex degree of coherence** (normalized):
γ(r₁, r₂, τ) = Γ(r₁, r₂, τ) / √[Γ(r₁, r₁, 0) Γ(r₂, r₂, 0)]
|γ| = 1: complete coherence. |γ| = 0: complete incoherence. 0 < |γ| < 1: partial.

**Visibility of interference fringes**:
V = (I_max − I_min)/(I_max + I_min) = |γ|

## Two Fundamental Theorems

### Wiener-Khinchin Theorem (Temporal Coherence)

Power spectrum S(ω) = FT of autocorrelation Γ(τ):
S(ω) = ∫ Γ(τ) e^{iωτ} dτ,   Γ(τ) = ⟨E(t+τ)E*(t)⟩

Coherence time τ_c ∼ 1/Δω (bandwidth). For quasi-monochromatic light:
τ_c ∼ λ²/(c·Δλ). Interference only for path difference < c·τ_c.

### van Cittert-Zernike Theorem (Spatial Coherence)

For a spatially incoherent source of intensity I(ξ,η):
γ(r₁, r₂, 0) = e^{iψ} ∫ I(ξ,η) e^{−ik(Δx·ξ+Δy·η)/R} dξdη / ∫ I dξdη

The complex degree of coherence is the FOURIER TRANSFORM of the source
intensity distribution. This is the foundation of stellar interferometry
(Michelson): measure γ → infer source angular size.

**Coherence area**: A_c ∼ (λR)²/A_source. Two points on a detection plane
produce interference only if separated by less than ∼√A_c.

## Examples

**Young's double slit with extended source**: Fringe visibility drops as
source size increases. Critical source size: w_crit ∼ λR/d (slit separation d).

**Stellar interferometry**: For a uniform disk star of angular diameter θ,
γ(d) = 2J₁(πθd/λ)/(πθd/λ). First zero at d = 1.22λ/θ → measure d where
fringes disappear → θ.

## Connection to Fluctuation-Dissipation

The mutual coherence function is the CLASSICAL analog of the quantum
correlation function ⟨x̂(t)x̂(0)⟩ in `reasoning.fluctuation_dissipation_quantum`.
Both are statistical second moments encoding how correlations decay in
time and space.

## Cross-References

- Born & Wolf §10.2-10.4
- landau-graph: reasoning.fluctuation_dissipation_quantum (quantum analog)
