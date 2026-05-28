---
skill_id: knowledge.continuous.spatial_dispersion
type: knowledge
summary_50t: >
  ε_ik(ω,k) = ε_t(δ_ik−k_i k_k/k²) + ε_l k_i k_k/k². ε_l(k,ω) ≠ ε_t(k,ω)
  when k≠0. New waves possible (longitudinal, additional transverse).
  Natural optical activity from ε_ik ∝ e_ikl k_l.
trigger:
  - nonlocal dielectric response
  - longitudinal vs transverse waves in media
  - optical activity, gyrotropy
reasoning_role: nonlocal_dielectric
parent: reasoning.spatial_dispersion
retrieval_cost: 1
---

# knowledge.continuous.spatial_dispersion

**Nonlocal response**: D_i(r) = ∫ ε_ik(r−r') E_k(r') dV'.
For plane waves: D_i = ε_ik(ω,k) E_k.

**Tensor structure** (isotropic + inversion symmetry):
ε_ik = ε_t (δ_ik − k_i k_k/k²) + ε_l k_i k_k/k².

**Longitudinal waves**: D = ε_l E, div D = 0 → ε_l = 0 determines dispersion.
Transverse waves: ε_t = c²k²/ω² determines dispersion.

**New phenomena from spatial dispersion**:
- Additional light waves (e.g., Pekar waves in exciton region)
- Natural optical activity: ε_ik = ε(ω)δ_ik + iγ(ω)e_ikl k_l → circular birefringence
- Gyrotropy: rotation of polarization plane in optically active media

**Plasma**: ε_l(k,ω) from Vol.10 §29. Debye screening: ε_l(k,0) = 1 + 1/(ka_D)².
Longitudinal plasma oscillations: ε_l(k,ω) = 0 → ω = ω_p + 3k²v_T²/2ω_p.

**Symmetry**: ε_ik(ω,k) = ε_ki(ω,−k) (Onsager). For fixed k: analytic in UHP ω.

**Poynting vector** (§103, (103.15)): Spatial dispersion adds a new term:
S̄ = (c/8π)Re[E*×B] − (ω/16π)(∂ε_ik/∂k)E_i*E_k.
Energy flux direction is modified by ∂ε/∂k — a qualitatively new effect.

- Landau Vol.8 §103-106
