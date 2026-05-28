---
skill_id: knowledge.kinetic.landau_collision_integral
type: knowledge
summary_50t: >
  Fokker-Planck for Coulomb collisions: St f = −∂s_α/∂p_α.
  s_α = Σ∫ B_{αβ}(f∂f₁/∂p₁β − f₁∂f/∂p_β)d³p₁. Dominated by small-angle scattering.
  Coulomb logarithm L = ln(a_D/r_min) ~ 10-30.
trigger:
  - Coulomb collisions in plasma
  - electron-ion energy transfer
  - runaway electrons
reasoning_role: coulomb_collision_operator
parent: reasoning.collision_integral_construction
retrieval_cost: 1
---

# knowledge.kinetic.landau_collision_integral

**Why special for plasma**: Coulomb force is long-range → many distant
encounters (small-angle scattering) dominate over rare close collisions.
→ Collision integral takes Fokker-Planck form (diffusion in velocity space).

**Landau form** (§41):
```
St f_a = −Σ_b (∂/∂p_α)∫ B_{αβ}(u)[f_a ∂f_b/∂p'_β − f_b ∂f_a/∂p_α] d³p'
B_{αβ} = (2πe_a²e_b²L/m_a)(u²δ_{αβ} − u_αu_β)/u³
u = v − v',  L = Coulomb logarithm
```

**Coulomb logarithm**: L = ln(ρ_max/ρ_min), ρ_max = a_D, ρ_min = e²/T.
Typically L ~ 10-30 for laboratory and astrophysical plasmas.

**Relaxation times**:
```
τ_ee ~ m^{1/2}T_e^{3/2}/(ne⁴L)    (electron-electron)
τ_ei ~ M T_e^{3/2}/(m^{1/2}nZ²e⁴L) (electron-ion, ≫ τ_ee)
```

**Runaway electrons** (§45): Electric field E > E_c = ne³L/T → electrons
continuously accelerated (drag decreases with velocity ∝ 1/v²).

- Landau Vol.10 §41-45
