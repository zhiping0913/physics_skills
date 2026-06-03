---
skill_id: knowledge.em.coherence_interference
type: knowledge
summary_50t: >
  Young: Δφ=2πd sin θ/λ. Michelson: ΔL=λ/2 per fringe. Fabry-Perot:
  T=(1+4R sin²δ/(1−R)²)⁻¹, finesse F=π√R/(1−R). FTIR: evanescent coupling.
  HBT intensity interferometry: ⟨I(t)I(t+τ)⟩→|γ(τ)|².
trigger:
  - analyzing interferometer fringe patterns
  - designing optical cavities, etalons
reasoning_role: interference_knowledge
parent: reasoning.em.optical_coherence
retrieval_cost: 1
---

# knowledge.em.coherence_interference

**Young's double slit**: I = I₁+I₂+2√(I₁I₂)|γ|cos Δφ. Fringe spacing: Δy=λR/d.

**Michelson interferometer**: ΔL = Nλ/2 (N fringes). Used in: FTIR spectroscopy,
gravitational wave detection (LIGO: ΔL∼10⁻¹⁸m), stellar interferometry.

**Fabry-Perot etalon** (two parallel mirrors, reflectivity R, spacing L):
Transmission: T = T_max/[1+(2F/π)² sin²(δ/2)], δ=4πnL cos θ/λ.
Free spectral range: FSR=c/(2nL). Finesse: F=π√R/(1−R) (mirror-limited).
Resolving power: λ/Δλ = F·(2nL/λ). A F=100 etalon with L=1cm has R∼10⁷.

**Frustrated total internal reflection (FTIR)**: Two prisms separated by
gap d ≪ λ. Evanescent field couples across gap → transmission ∝ e^{−κd}.
Used in: beam splitters, near-field scanning optical microscopy (NSOM).

**Anti-reflection coating**: Single λ/4 layer n_coat=√(n_sub) → zero reflection
at design λ. Multilayer: Bragg reflector (alternating high/low n, λ/4 each).

**Hanbury Brown-Twiss (HBT)**: Intensity interferometry — correlate photocurrents
from two detectors: ⟨ΔI₁(t)ΔI₂(t+τ)⟩ ∝ |γ(r₁,r₂,τ)|². Measures |γ|², NOT γ→
works even when atmospheric turbulence randomizes phase. Used to measure stellar
diameters (Sirius: θ≈0.0063 arcsec → D∼1.7D_sun).

- Born & Wolf §7, §10; Griffiths §9
