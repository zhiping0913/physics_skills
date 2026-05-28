---
skill_id: knowledge.continuous.moving_media_electrodynamics
type: knowledge
summary_50t: >
  D + (v/c)×H = ε(E + (v/c)×B), B + (E/c)×v = μ(H + (D/c)×v).
  Minkowski equations for moving media. Fresnel drag. Foundation for ROM.
trigger:
  - moving dielectric or conducting medium
  - relativistic plasma mirror boundary conditions
  - Fresnel drag, rotating media
reasoning_role: moving_media
parent: knowledge.continuous.dielectric_dispersion
retrieval_cost: 1
---

# knowledge.continuous.moving_media_electrodynamics

**4-tensor foundation** (§76): D and H form a 4-tensor H_μν (76.5),
not just vectors. Along with the field tensor F_μν, this gives the
relativistic formulation: ∂H^{λμ}/∂x^μ = 0, ∂F_{λμ}/∂x^ν + cyclic = 0.

**Exact Minkowski equations** (76.9, valid at any v/c):
```
D + [v×H]/c = ε(E + [v×B]/c)
B + [E×v]/c = μ(H + [D×v]/c)
```

**Linearized in v/c** (76.10-76.11):
```
D = εE + (εμ−1)[v×H]/c
B = μH + (εμ−1)[E×v]/c
```

**Boundary conditions** at moving interface (76.13-76.14):
[n,E₂−E₁] = (v_n/c)(B₂−B₁),  [n,H₂−H₁] = −(v_n/c)(D₂−D₁).
Linearized: [n,E₂−E₁] = (v_n/c)(μ₂−μ₁)H_t, etc.

**Caveat** (§76 footnote): The Minkowski formulation neglects weak effects
from velocity gradients (gyromagnetic effects, cf. §36).

**Fresnel drag**: Light in moving medium with refractive index n.
Phase velocity: c/n ± v(1 − 1/n²). Fizeau experiment.

**ROM application**: Relativistic plasma mirror. Moving plasma-vacuum
boundary at near-light speed. In the mirror rest frame: incident wave
reflected with Doppler shift → high harmonics.

- Landau Vol.8 §76
