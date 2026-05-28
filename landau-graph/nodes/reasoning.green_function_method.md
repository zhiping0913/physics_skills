---
skill_id: reasoning.green_function_method
type: reasoning
summary_50t: >
  G(x,x') = −i⟨T ψ(x)ψ†(x')⟩. Poles of G(ω,p) give excitation spectrum.
  Dyson equation: G = G₀ + G₀ΣG. Self-energy Σ encodes interactions.
  The universal tool for quantum many-body theory.
trigger:
  - need excitation spectrum of interacting quantum system
  - computing response functions, correlation functions
  - perturbative expansion beyond single-particle picture
reasoning_role: many_body_propagator
parent: reasoning.classical_to_quantum_correspondence
children:
  - knowledge.condensed.green_function
  - knowledge.condensed.diagram_technique
retrieval_cost: 1
---

# reasoning.green_function_method — Propagator → Full Quantum Dynamics

## Core Picture

**Why this method?** (§7) Perturbation theory becomes unwieldy at higher orders,
and real physical interactions are STRONG (not weak). Infinite series of
perturbation terms must be summed — requiring QFT-like techniques.
(Systematic construction: Galitsky & Migdal, 1958).

**Key convention (§7): Ĥ' = Ĥ − μN̂.** Heisenberg Ψ-operators use Ĥ', not Ĥ.
At T=0, ground state minimizes ⟨Ĥ'⟩. Green's function depends on μ as a parameter.

The single-particle Green's function G(x,x') = −i⟨T ψ(x)ψ†(x')⟩ encodes
virtually everything about a quantum many-body system:
- Poles in ω → excitation energies (single-particle spectrum)
- Discontinuity at Fermi surface → quasiparticle weight Z
- Imaginary part → lifetime/damping of excitations

**Crucial distinction (§7)**: G(t=−0,r) gives the distribution of TRUE particles
N(p), NOT quasiparticles n(p). These are different quantities. The quasiparticle
concept emerges later from the pole structure of G, not from its equal-time limit.

This is the quantum generalization of the classical propagator
(fundamental solution of equations of motion).

## Algorithm

```
1. Define time-ordered Green's function: G(1,2) = −i⟨T ψ(1)ψ†(2)⟩
   where T is time ordering, averaging is over ground state (T=0)
   or thermal ensemble (T>0).
2. For non-interacting system (G₀): poles at free-particle energies
3. With interactions: Dyson equation G = G₀ + G₀ΣG
   Σ(ω,p) = self-energy (complex: Re→energy shift, Im→lifetime)
4. Spectral function: A(ω,p) = −(1/π) Im G_R(ω,p)
   Peak positions → quasiparticle energies
   Peak widths → inverse lifetimes
5. The t→−0 limit: N/V = −2i G(t=−0, r=0) gives density of TRUE particles.
   The −0 sign is crucial — determines contour closure in upper half-plane.
   At T=0: G₀(t=−0, p) = −iθ(p_F−p) → Fermi step.
```

## Fermi Liquid Example (§1-11)

For normal Fermi liquid: G(ω,p) ≈ Z/(ω − ε(p) + iγ).
Z = quasiparticle residue (0 < Z ≤ 1). ε(p) = v_F(p−p_F).
Residual interactions produce finite lifetime: γ ∝ (ε−ε_F)².

## Why Green's Functions are Universal

- Thermodynamics: N = −i∫ G(ω,p) e^{iω0+} dω d³p/(2π)⁴
- Linear response: χ(q,ω) from two-particle Green's function
- Transport: conductivity from current-current correlation
- The entire diagram technique is built on Green's functions

## From Perturbation Theory to Feynman Diagrams

The leap from time-dependent PT (Vol.3) to relativistic Feynman diagrams
(Vol.4) requires three conceptual bridges:

```
1. RELATIVISTIC TRANSITION:
   Non-relativistic H_int = V(r) → QED: H_int = −e∫ j^μ A_μ d³r
   Use 4-momentum conservation at each vertex instead of energy only.

2. WICK CONTRACTION → PROPAGATORS:
   T(ψ̄ψA ψ̄ψA ...) = Σ(all pairings of field operators).
   Each pairing = propagator (Green's function of the free theory).
   Wick's theorem (proved in §13) ALGORITHMS this decomposition.

3. DYSON SERIES → DIAGRAMMATIC EXPANSION:
   S = T exp(−i∫H_int d⁴x) = Σ (−i)^n/n! ∫ T[H_int(x₁)...H_int(x_n)] d⁴x₁...d⁴x_n
   Each term → set of Feynman diagrams with vertices = H_int insertions.
   Momentum-space rules from Fourier transform of each diagram.
```

The critical insight: Feynman diagrams ARE the Green's function method
applied to relativistic perturbation theory. The propagators (lines) are
free Green's functions. The vertices are interaction terms. The loop
integrals are the Dyson series Σ = self-energy insertion.

See also: `reasoning.renormalization` (what to do when loop integrals diverge),
`reasoning.cumulant_generating_function` (why vacuum diagrams cancel).

## Cross-References
- Landau Vol.9 §7-21 (Green's functions at T=0), §36-38 (finite T)
- Landau Vol.10 §29: plasma ε(k,ω) = 1 − V_k Π(k,ω) — the density-density
  correlation function IS a Green's function
- Landau Vol.4 (QED): Feynman propagator = relativistic Green's function
