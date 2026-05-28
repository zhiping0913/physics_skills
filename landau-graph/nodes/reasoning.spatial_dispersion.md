---
skill_id: reasoning.spatial_dispersion
type: reasoning
summary_50t: >
  D(r) depends on E(r') in a neighborhood → ε = ε(ω,k) tensor.
  Even in isotropic media: ε_ik = ε_t(δ_ik − k_i k_k/k²) + ε_l k_i k_k/k².
  Spatial dispersion ∝ a/λ, small but produces qualitatively new effects.
trigger:
  - nonlocal medium response
  - λ comparable to correlation length
  - need longitudinal vs transverse response
reasoning_role: nonlocal_response
parent: reasoning.causality_to_analyticity
children:
  - knowledge.continuous.spatial_dispersion
retrieval_cost: 1
---

# reasoning.spatial_dispersion — Nonlocality → ε(ω,k)

## Core Picture

In general, the polarization at r depends on the field in a finite region
around r. For plane waves: D_i = ε_ik(ω,k) E_k. The k-dependence
(spatial dispersion) is typically small (∝ a/λ), but produces qualitatively
NEW effects that are absent in the local (k→0) limit.

## Key Structure

**Why no B-term in (103.1)**? E and B are not independent — linked by Maxwell:
rot E = iωB/c. Dependence on B = dependence on spatial derivatives of E
= already captured by ε_ik(k). No separate magnetic term needed.

**Convention**: With spatial dispersion it is convenient to set M=0, B=H,
absorbing all averaged microscopic currents into D. The connection between
(ε_l,ε_t) and (ε,μ) at k→0 is given in Problem 1 of §103.

In isotropic media with inversion symmetry:
```
ε_ik(ω,k) = ε_t(ω,k)(δ_ik − k_i k_k/k²) + ε_l(ω,k) k_i k_k/k²
```
ε_l: longitudinal permittivity (E ∥ k)
ε_t: transverse permittivity (E ⟂ k)
ε_l(ω,0) = ε_t(ω,0) = ε(ω) (local limit)

## When Spatial Dispersion Matters

- **Plasma**: Debye screening → nonlocality on scale a_D (can be macroscopic)
- **Metals at low T**: anomalous skin effect (electron mean free path > skin depth)
- **Natural optical activity**: ε_ik(ω,k) has antisymmetric part ∝ k → rotation of
  polarization (circular birefringence)
- **Exciton-polaritons**: additional light waves from spatial dispersion

## Relation to Vol.10 Plasma ε

Vol.10 derived ε_l(k,ω) from the Vlasov equation — that is a MICROSCOPIC
derivation. Vol.8 gives the MACROSCOPIC framework: the form of ε_ik(k,ω)
from symmetry + analyticity, independent of the specific microscopic model.

## Analytical Properties

For fixed k: ε_ik(ω,k) is analytic in upper half-plane, satisfies
Kramers-Kronig. **Crucially: ε_l(k,ω) at k≠0 does NOT diverge at ω→0 even
in conductors** — the ω=0 pole is an artifact of the local (k=0) approximation
(§103). No subtraction needed in KK for ε_l(k≠0).

## Key Qualitative Effects

- **Poynting vector modification** (§103): S̄ = (c/8π)Re[E*×B] − (ω/16π)(∂ε_ik/∂k)E_i*E_k.
  The energy flux direction is altered by spatial dispersion — a qualitatively
  new effect absent in local media.

## Cross-References
- Landau Vol.8 §103-106 (spatial dispersion, optical activity)
- Landau Vol.10 §29 (plasma ε(k,ω) from Vlasov — microscopic derivation)
- Landau Vol.8 §77-82 (frequency dispersion, Kramers-Kronig)
