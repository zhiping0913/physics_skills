---
skill_id: knowledge.kinetic.landau_damping_formula
type: knowledge
summary_50t: >
  ε_l = 1 − (4πe²/k²)∫(k·∂f/∂p)/(kv−ω−i0) d³p. Im ε ∝ df/dv at v=ω/k.
  Maxwellian: γ ∝ exp(−ω²/2k²v_T²). Landau 1946. Collisionless!
trigger:
  - damping rate of plasma wave
  - Landau damping in collisionless plasma
  - wave-particle resonance
reasoning_role: collisionless_damping_formula
parent: reasoning.landau_damping
retrieval_cost: 1
---

# knowledge.kinetic.landau_damping_formula

**Longitudinal dielectric function** (any isotropic f₀):
ε_l(k,ω) = 1 − (4πe²/k²)∫(k·∂f/∂p)/(kv−ω−i0) d³p.
= 1 − (4πe²/k)∫(df(p_x)/dp_x)/(kv_x−ω−i0) dp_x.

**Landau's rule**: ω → ω + i0 (causality: field turned on adiabatically).
```
1/(kv−ω−i0) = P(1/(kv−ω)) + iπ δ(kv−ω)
```

**Imaginary part**: ε_l'' = −(4π²e²m/k²)(df/dp_x)|_{v_x=ω/k}.
For Maxwellian: Im ε_l ∝ exp(−ω²/2k²v_T²).

**Damping rate** (weak damping, |γ| ≪ ω):
γ = −ε_l''/(∂ε_l'/∂ω) ≈ −√(π/8) ω_p (ω_p/kv_T)³ exp(−ω_p²/2k²v_T²).

**Physical mechanism**: Energy transfer to resonant particles (v ≈ ω/k).
More slow particles than fast ones in Maxwellian → net damping.
Inverse Landau damping: df/dv > 0 → instability (beam-plasma).

**Plasma echo** (§35): Reversible! Damped wave information stored in
fine-grained f(v), can be recovered by a second pulse.

- Landau Vol.10 §30
