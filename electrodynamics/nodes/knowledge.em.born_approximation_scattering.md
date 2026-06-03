---
skill_id: knowledge.em.born_approximation_scattering
type: knowledge
summary_50t: >
  Weak scatterer: f(k,k')∝∫δε(r')e^{i(k−k')·r'}dV'. Condition: |δε/ε|≪1,
  phase shift ≪π across target. RDG (dielectric): same form, valid for |m−1|≪1.
  Eikonal: small-angle, high-E, phase=∫(n−1)k₀dz. Contrast with Mie exact.
trigger: weak scattering from irregular objects, soft biological tissue
reasoning_role: born_scattering
parent: reasoning.em.scattering_cross_section
retrieval_cost: 1
---

# knowledge.em.born_approximation_scattering

**Born approximation** (Jackson §10.4, Bohren §7): For a weak scatterer with
dielectric contrast Δε(r)=ε(r)−ε₀, the scattering amplitude is:

f(k,k') = (k²/4π) ∫ Δε(r)/ε₀ e^{i(k−k')·r} dV

The scattered field is the FOURIER TRANSFORM of the dielectric contrast
evaluated at the momentum transfer q=k−k'. |q|=2k sin(θ/2).

**Validity**: |Δε/ε₀|≪1 AND phase shift across target Δφ=∫|k Δn| dz ≪ π.
For spherical target radius a: |m−1|ka ≪ 1.

**Rayleigh-Debye-Gans (RDG)**: same form for dielectric scatterers where
n(r)≈n₀+Δn(r). Gives I(q)∝P(q) (particle form factor). For sphere:
P(q)=[3(sin u−u cos u)/u³]², u=qa. Guinier: I(q)∝exp(−q²R_g²/3) for qR_g≪1.

**Eikonal approximation** (small-angle, high-E): ψ=e^{ik₀z} exp(i∫(n−1)k₀dz).
Valid when λ≪a and Δn≪1. Used for atmospheric propagation, plasma diagnostics.

**Contrast with Mie**: Mie = exact for homogeneous sphere (all ka, all m).
Born = approximate for arbitrary shape, weak contrast. Born fails when
resonances are present (Mie resonances at ka∼1 for m≳1.5).

- Jackson §10.4, Bohren §7
