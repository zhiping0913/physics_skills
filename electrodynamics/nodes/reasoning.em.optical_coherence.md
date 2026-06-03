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
parent: landau-graph:reasoning.fluctuation_dissipation_quantum
sign_convention: stationary random process; ⟨·⟩ = ensemble/time average; complex analytic signal representation
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

## Derivation Sketch

Starting from `landau-graph: reasoning.fluctuation_dissipation_quantum` we have
the quantum correlation function ⟨x̂(t)x̂(0)⟩ encoding statistical fluctuations
and the fluctuation-dissipation theorem linking correlations to response. The
classical optical analog is the mutual coherence function:

Γ(r₁, r₂, τ) = ⟨E(r₁, t+τ) E*(r₂, t)⟩

where E is the complex analytic signal (positive-frequency part of the real
field). This is a second-order correlation function; higher-order correlations
g₁(τ), g₂(τ) distinguish thermal from coherent and non-classical light.

**Key non-obvious step — van Cittert-Zernike theorem**: An extended spatially
INCOHERENT source (each surface element emits independently) produces a
partially COHERENT field at a distant plane. The complex degree of coherence
γ(r₁, r₂) is the normalized Fourier transform of the source intensity
distribution I(ξ,η):

γ(Δx, Δy) = e^{iψ} ∬ I(ξ,η) e^{−ik(ξΔx+ηΔy)/R} dξdη / ∬ I(ξ,η) dξdη

This holds because each source point radiates a spherical wave; the
superposition at the observation plane creates a random field whose
correlation function is the Fourier transform of the source intensity
(Wiener-Khinchin in space). The theorem is the foundation of aperture
synthesis in radio astronomy and stellar interferometry.

**Coherent vs partially coherent imaging (Hopkins formulation)**:
For a Köhler-illuminated microscope, the image intensity is:
I(x) = ∭ TCC(f₁,f₂) Õ(f₁) Õ*(f₂) e^{2πi(f₁−f₂)x} df₁ df₂
where the transmission cross-coefficient TCC encodes the illumination
partial coherence. Two limits: (1) coherent illumination (point source) →
linear in amplitude — edge ringing, speckle; (2) incoherent illumination
(large source) → linear in intensity — smooth, no speckle. The cutoff
frequency is 2NA/λ (incoherent) vs NA/λ (coherent) — a factor of 2
resolution gain for incoherent imaging (Hopkins, Proc. Roy. Soc. 1953).

**Speckle statistics**: When coherent light scatters from a rough surface
(surface roughness > λ), the random phase at each scattering point produces
a speckle pattern. For fully developed speckle (many independent scatterers):
intensity follows negative-exponential PDF p(I) = (1/⟨I⟩)e^{−I/⟨I⟩};
contrast C = σ_I/⟨I⟩ = 1 (fully developed). Speckle size is λz/D
(diffraction-limited). Speckle interferometry exploits these statistics
for high-resolution imaging through turbulence (Labeyrie technique).

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

## Edge Cases

- **Coherence collapses under strong turbulence**: When the atmospheric
  coherence time τ_0 (Greenwood time) < detector integration time, the
  fringe visibility washes out. Remedy: adaptive optics (wavefront
  correction at > 1/τ_0) or speckle interferometry (short-exposure
  lucky imaging) rather than long-exposure averaging.
- **Laser coherence is NOT perfect**: Lasers have finite linewidth
  (Schawlow-Townes limit Δν ∝ 1/P) and drift. For long-baseline
  interferometry (> coherence length L_c = c/Δν), coherence breaks down —
  use active path-length stabilization or heterodyne detection with
  independent local oscillators.
- **Non-classical light breaks the classical bounds**: |γ(τ)| ≤ 1 is a
  classical constraint. Squeezed light and entangled photons can achieve
  sub-shot-noise correlations; for these, switch to the full quantum
  optical description (Glauber g⁽²⁾, Mandel Q-parameter).

## Connection to Fluctuation-Dissipation

The mutual coherence function is the CLASSICAL analog of the quantum
correlation function ⟨x̂(t)x̂(0)⟩ in `reasoning.fluctuation_dissipation_quantum`.
Both are statistical second moments encoding how correlations decay in
time and space.

## Cross-References

- Born & Wolf §10.2-10.4
- landau-graph: reasoning.fluctuation_dissipation_quantum (quantum analog)
