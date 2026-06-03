---
skill_id: knowledge.plasma.wave_mode_atlas
type: knowledge
summary_50t: >
  CMA diagram complete. R-wave: N²=R, ω_ce resonance, ω_R cutoff, whistler
  ω∝k². L-wave: ω_ci resonance, ω_L cutoff. O-mode: N²=P, ω_p cutoff. X-mode:
  N²=RL/S, ω_UH, ω_LH resonances. Alfvén: N²=c²/v_A². Helicon: N²∝ω_p²/ωω_ce.
  Accessibility: between cutoffs. Mode conversion at resonances (Budden tunnelling).
trigger: identifying all cold-plasma wave modes and their propagation windows
reasoning_role: wave_atlas
parent: reasoning.plasma.dielectric_tensor_magnetized
retrieval_cost: 1
---

# knowledge.plasma.wave_mode_atlas

**CMA diagram** (Stix §1-2, Ginzburg §3-5): parameter space (ω_p²/ω², ω_c/ω)
→ 13 topologically distinct regions. Each region has different number of
propagating modes, resonance cone angles, and accessibility windows.

| Mode | ∥/⊥ B₀ | N² expression | Cutoff | Resonance |
|------|---------|---------------|--------|-----------|
| R (whistler) | ∥ | R | ω_R=ω_ce/2+√(ω_p²+ω_ce²/4) | ω_ce |
| L (ion cycl.) | ∥ | L | ω_L | ω_ci |
| O (ordinary) | ⊥ | P | ω_p | — |
| X (extraordinary) | ⊥ | RL/S | ω_R, ω_L | ω_UH=√(ω_p²+ω_ce²), ω_LH |
| Alfvén | ∥ | c²/v_A² | — | — |
| Helicon | ∥ | ω_p²/ωω_ce | — | — |

**Whistler** (ω_ci≪ω≪ω_ce): N²≈ω_p²/(ω ω_ce), ω∝k², v_g=2v_p.
Lightning whistlers: dispersion→chirp. Lab: helicon sources.

**Mode conversion**: X-mode at ω_UH→electron Bernstein wave (EBW).
O-mode at ω_p→Langmuir wave. Budden tunnelling: wave incident on
cutoff-resonance pair → partial transmission through evanescent region.

**Accessibility**: wave can only propagate where N²>0. For EC heating,
choose ω, θ such that wave reaches cyclotron resonance before cutoff.

- Stix §1-6, Ginzburg §3-8
