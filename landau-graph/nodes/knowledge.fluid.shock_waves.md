---
skill_id: knowledge.fluid.shock_waves
type: knowledge
summary_50t: >
  Rankine-Hugoniot: [ρv_n]=0, [p+ρv_n²]=0, [w+v²/2]=0 across shock.
  Shock adiabat: ε₂−ε₁ + (p₁+p₂)(V₂−V₁)/2 = 0. Entropy always increases.
  Weak shocks → sound waves. Strong shocks → T₂/T₁ ≫ 1.
trigger:
  - supersonic flow, shock formation
  - Rankine-Hugoniot jump conditions
  - shock heating in plasma
reasoning_role: nonlinear_wave_discontinuity
parent: knowledge.fluid.euler_equation
retrieval_cost: 1
---

# knowledge.fluid.shock_waves

**Shock = surface of discontinuity** in compressible flow.
Mass, momentum, energy fluxes must be continuous across it.

**Rankine-Hugoniot conditions** (§84-85):
```
[ρv_n] = 0              mass flux
[p + ρv_n²] = 0          normal momentum flux
ρv_n[v_t] = 0            tangential momentum (v_t continuous)
ρv_n[w + v²/2] = 0       energy flux
```
[v_n] means jump across shock. w = ε + pV = specific enthalpy.

**Shock adiabat** (Hugoniot):
ε₂ − ε₁ + ½(p₁+p₂)(V₂−V₁) = 0. Relates states on either side.

**For polytropic gas** (p ∝ ρ^γ):
ρ₂/ρ₁ = (γ+1)M₁²/[(γ−1)M₁²+2]. Maximum compression: (γ+1)/(γ−1).
For γ=5/3: max compression = 4.

**Entropy**: ALWAYS increases across shock (irreversible).
s₂ − s₁ ∝ (M²−1)³ for weak shocks.

**Weak shocks**: Speed → sound speed. Width determined by viscosity.
**Strong shocks**: T₂/T₁ ∝ M₁². Ionization, radiation important.

- Landau Vol.6 §84-95
