---
skill_id: reasoning.plasma.transport_coefficients
type: reasoning
summary_50t: >
  Collisions → transport. Magnetized: χ⊥≪χ∥ (∝B₀⁻²). Classical (Braginskii)
  → neoclassical (banana, plateau, Pfirsch-Schlüter) → anomalous (turbulent).
  Bootstrap current from ∇p in toroidal geometry. Scaling: τ_E ∼ I_p P^{−α}.
trigger:
  - computing heat/particle/momentum transport in magnetized plasma
  - understanding confinement scaling for fusion
reasoning_role: transport
parent: reasoning.kinetic_equation_closure
retrieval_cost: 1
references:
  - landau-graph: reasoning.kinetic_equation_closure
---

# reasoning.plasma.transport_coefficients — Collisions → Confinement

## Core Picture

In magnetized plasma, transport ACROSS B₀ is suppressed: χ⊥ ∝ 1/B₀²
(classical), or determined by toroidal geometry (neoclassical), or by
turbulence (anomalous — dominant in fusion plasmas).

## Classical Transport (Braginskii, Chen §5)

From the two-fluid moment equations with collisions:

```
η_∥ = (m_e ν_ei)/(n e²)  (Spitzer resistivity, SI: η_∥ ≈ 5.2×10⁻⁵ Z lnΛ / T_e[eV]^{3/2} Ω·m)
χ_e∥ ≈ 3.2 n_e T_e/(m_e ν_ei)    (parallel electron thermal)
χ_e⊥ = χ_e∥/(1+ω_ce²/ν_ei²)     (⊥ suppressed by magnetization)
D_⊥ = η_∥ n T/B₀²                (classical particle diffusion)
```

## Neoclassical Transport (Chen §5, Wesson §3)

Toroidal geometry traps particles (banana orbits) → enhanced transport:

| Regime | Collisionality ν* = ν qR/v_th ε^{3/2} | χ scaling |
|--------|---------------------------------------|-----------|
| Banana | ν* ≪ 1 | χ ∼ q² ε^{−3/2} χ_classical |
| Plateau | ν* ∼ 1 | χ ∼ (T/B₀R) ρ_i² ν |
| Pfirsch-Schlüter | ν* ≫ 1 | χ ∼ q² χ_classical |

**Bootstrap current**: toroidal current driven by ∇p, no external loop voltage:
j_BS ∼ (ε^{1/2}/B_θ) dp/dr. Essential for steady-state tokamak operation.

## Anomalous (Turbulent) Transport

Always dominant in fusion plasmas. Mixing-length estimate:
D_turb ∼ γ/k_⊥² where γ, k_⊥ from dominant microinstability (ITG, TEM, ETG).
Empirical scaling: τ_E ∝ I_p^α P^{−β} n^{γ} (e.g., IPB98(y,2)).

## Cross-References

- Chen §5, Wesson §3, Braginskii (1965)
- landau-graph: reasoning.kinetic_equation_closure (moments + closure → transport)
