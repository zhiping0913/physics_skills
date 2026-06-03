---
skill_id: knowledge.plasma.mhd_waves_stability
type: knowledge
summary_50t: >
  Alfvén: ω²=k_∥²v_A². Magnetosonic: fast/slow. q(r)=rB_φ/RB_θ.
  Kruskal-Shafranov: q>1. β_N<3.5. Tearing Δ'>0. Sawtooth (m=1,n=1).
  ELMs (peeling-ballooning). RWM (n=1, wall-stabilized).
trigger: computing MHD wave dispersion, stability analysis for tokamak
reasoning_role: mhd_knowledge
parent: reasoning.plasma.mhd_equilibrium_stability
retrieval_cost: 1
---

# knowledge.plasma.mhd_waves_stability

**MHD waves** (uniform B₀, homogeneous):
Alfvén: ω² = k_∥² v_A², v_A = B₀/√(μ₀ρ). Torsional, incompressible.
Fast/slow magnetosonic: ω²=(k²/2)[c_s²+v_A²±√((c_s²+v_A²)²−4c_s²v_A²cos²θ)].
Slow: ∝cos²θ, fast: isotropic at c_s≪v_A.

**Tokamak stability**:
Safety factor: q(r)=rB_φ/RB_θ. q₀<1 → sawtooth. q₉₅>1 for kink.
β limit: β_N = β(%) a(m) B₀(T)/I_p(MA) < 3.5 (Troyon).
Greenwald density limit: n_G = I_p/πa² [10²⁰m⁻³].

**Tearing mode**: Δ'=[ψ'/ψ]_r_s⁺−[ψ'/ψ]_r_s⁻. Δ'>0 → unstable.
Rutherford growth: initially exponential → saturated island width w∝t.
NTM: bootstrap current perturbation → seed island required.

**ELMs** (Edge Localized Modes): peeling-ballooning instability.
Type I (large, low f): ideal ballooning at edge, ΔW_ELM≈3-10% W_ped.

- Friedberg §4-13, Chen §6, Wesson §6-7
