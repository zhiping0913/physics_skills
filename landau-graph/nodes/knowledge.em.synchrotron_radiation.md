---
skill_id: knowledge.em.synchrotron_radiation
type: knowledge
summary_50t: >
  Ultra-relativistic (γ≫1) charge in magnetic field radiates in a narrow
  forward cone θ~1/γ. Spectrum peaks at ω_c ~ γ³ω₀. Total power ∝ γ².
  Fundamental for astrophysics and laser-plasma HHG.
trigger:
  - ultra-relativistic charge in B field
  - high-energy astrophysical radiation
  - relativistic HHG harmonics
reasoning_role: relativistic_radiation
parent: knowledge.em.lienard_wiechert
retrieval_cost: 1
---

# knowledge.em.synchrotron_radiation

**Key parameters**:
```
ω₀ = eB/γmc     gyration frequency
ω_c = (3/2)γ³ω₀  critical frequency (spectrum peak ~0.3ω_c)
```

**Total power**: I = (2e⁴B²/3m²c³)γ² = (2e²c/3R²)γ⁴
(R = curvature radius of trajectory)

**Angular distribution**: Narrow cone of opening angle Δθ ~ 1/γ
in the instantaneous velocity direction.

**Spectrum** (continuous for single charge):
```
dI/dω ∝ (ω/ω_c) ∫_{ω/ω_c}^∞ K_5/3(x) dx
```
Low frequencies: dI/dω ∝ ω^{1/3}. High: exponential cutoff at ω ~ ω_c.

**Why γ³ appears**: The radiation pulse seen by observer is shortened by
two relativistic effects: (1) the charge moves toward observer → Doppler,
(2) radiation is beamed in 1/γ cone → observer sees only a fraction of orbit.
Combined → pulse duration ∝ 1/γ³ω₀ → spectrum extends to ω_c ∝ γ³ω₀.

- Landau Vol.2 §74
