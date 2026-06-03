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

## Derivation Sketch (from kinetic closure → transport tensors)

Starting from `landau-graph: reasoning.kinetic_equation_closure` (which
establishes that kinetic equations truncated at finite moments require
closure relations — the stress tensor Π and heat flux q), the transport
coefficients are the CLOSURE OUTPUTS:

1. **Braginskii's procedure** (Handbook of Plasma Physics Part 1):
   expand the distribution function f = f_M + f_1, solve the linearized
   kinetic equation with the Landau collision operator, compute the
   fluxes (particle flux Γ, heat flux q, momentum flux Π) in terms of
   the thermodynamic forces (∇n, ∇T, E*, R — where R is the friction
   force). KEY NON-OBVIOUS: the collision operator couples unlike species
   (electrons ↔ ions) through the friction force R, which is the
   momentum exchange between species.

2. **Full Braginskii transport tensor** (magnetized, two-fluid): the
   general form for particle and heat fluxes is:
   ```
   Γ_α = −D_α·∇n_α − n_α μ_α·E* − n_α δ_α·∇T_α
   q_α = −κ_α·∇T_α − n_α T_α φ_α·E* − T_α ν_α·∇n_α
   ```
   where each coefficient (D, μ, δ, κ, φ, ν) is a TENSOR with ∥, ⊥, ∧
   (Hall) components relative to B₀. For example, the perpendicular
   thermal conductivity: κ_e⊥ = κ_e∥/(1 + ω_ce²τ_ei²) and the off-diagonal
   (Righi-Leduc) heat flux: q_e∧ = (ω_ce τ_ei) κ_e⊥ (ĥ×∇T_e). These
   off-diagonal terms produce heat flux PERPENDICULAR to both ∇T and B —
   essential for understanding divertor heat loads and impurity transport.

3. **Gyrokinetic procedure** (modern, for turbulence): instead of
   fluid moments, solve the gyrokinetic Vlasov equation for the
   distribution function f(R, μ, v_∥) in 5D guiding-center phase space.
   The transport fluxes emerge as velocity-space moments of f, averaged
   over the turbulent fluctuations. KEY ADVANTAGE: the gyrokinetic
   ordering (ω/Ω_i ∼ k_∥/k_⊥ ∼ δf/f ≪ 1) removes the fast gyromotion
   analytically, reducing the problem from 6D to 5D and enabling
   simulations of turbulent transport at experimentally relevant
   parameters (ρ* ≡ ρ_i/a ∼ 10⁻³ is resolved).

4. **Neoclassical → turbulent bridge**: neoclassical theory provides
   the collisional (irreducible minimum) transport level. Any excess is
   ANOMALOUS (turbulent). The gyrokinetic equation combines both: the
   background (neoclassical) plus the fluctuation (turbulent) driven
   by microinstabilities (ITG, TEM, ETG). The quasilinear flux is:
   Γ ∼ Σ_k γ_k |φ_k|² / (ω_rk − ω_*)^2, where ω_* is the diamagnetic
   frequency that provides the free-energy drive.

## Classical Transport (Braginskii, Chen §5)

From the two-fluid moment equations with collisions:

```
η_∥ = (m_e ν_ei)/(n e²)  (Spitzer resistivity, SI: η_∥ ≈ 5.2×10⁻⁵ Z lnΛ / T_e[eV]^{3/2} Ω·m)
χ_e∥ ≈ 3.2 n_e T_e/(m_e ν_ei)    (parallel electron thermal)
χ_e⊥ = χ_e∥/(1+ω_ce²/ν_ei²)     (⊥ suppressed by magnetization)
D_⊥ = η_∥ n T/B₀²                (classical particle diffusion)
```

**Full Braginskii transport matrix** (magnetized electrons, summary):

| Flux | ∥ component | ⊥ component | ∧ (Hall) component |
|------|------------|------------|-------------------|
| Γ (particle) | −D_∥ ∇_∥ n | −D_⊥ ∇_⊥ n + D_∧ (ĥ×∇n) | E×B / curvature |
| q (heat) | −κ_∥ ∇_∥ T | −κ_⊥ ∇_⊥ T + κ_∧ (ĥ×∇T) | Righi-Leduc |
| Π (stress) | η₀ W_∥ | η₁ W_⊥ | η₂ (gyroviscosity) |

**Thermo-electric (off-diagonal) coefficients**:
- **Ettingshausen effect**: heat flux driven by electric field (φ term).
- **Nernst effect**: electric field/current from ∇T (δ, ν terms).
- **Thermo-power**: V_th = −∫ (δ_∥/σ_∥) ∇_∥ T_e · dl (Seebeck for plasma).
These off-diagonal terms dominate in the pedestal and divertor where
∇T is large and MHD equilibrium enforces specific current patterns.

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

**Gyrokinetic turbulence procedure**:
1. Compute axisymmetric equilibrium (Grad-Shafranov → flux surfaces).
2. Linear gyrokinetic analysis (GS2, GENE, GYRO): find unstable modes
   (ITG, TEM, ETG, KBM) with growth rates γ(k_θ ρ_i).
3. Nonlinear gyrokinetic simulation: evolve δf until saturated turbulence.
4. Compute fluxes: Γ = ⟨δn δv_E⟩, Q = ⟨δp δv_E⟩ as time averages.
5. Compare with experimental power-balance χ_eff.
6. When gyro-Bohm scaling (χ ∝ ρ*) breaks down → intrinsic size scaling
   indicates nonlocal effects (avalanches, profile stiffness).

## Edge Cases

- **Collisionless limit (ν* → 0)**: Braginskii's Chapman-Enskog expansion
  assumes small mean free path (ν_ei ≫ ω for any relevant process).
  When ν_ei → 0, the fluid closure breaks down — use the collisionless
  kinetic equation (Vlasov) with Landau damping as the dissipation
  mechanism. In practice, even "collisionless" fusion plasmas have enough
  collisions for Braginskii at the ion scale — but electron parallel
  transport at high T_e may need a kinetic treatment (Spitzer-Härm with
  electron-electron collisions run to convergence, or nonlocal when
  λ_ei > L_T).
- **Nonlocal transport (λ_mfp > L_T)**: in ICF hot spots and low-density
  tokamak edges, the electron mean free path exceeds the temperature
  scale length. The local Fourier law q = −κ∇T fails — heat flux at a
  point depends on the temperature profile over a region of size λ_mfp.
  Use the nonlocal transport model (Schurtz-Nicolaï-Busquet, SNB) or
  Vlasov-Fokker-Planck (VFP) codes like KIPP or IMPACT. Signature:
  preheat ahead of the conduction front that Fourier models miss.
- **Stochastic magnetic fields**: when magnetic islands overlap (Chirikov
  criterion), field lines become stochastic and parallel transport along
  the tangled field dominates: χ_eff ∼ D_M χ_∥, where D_M = (δB_r/B)² L_c
  is the magnetic diffusion coefficient. Breaks down when the parallel
  correlation length L_c is shorter than the collisional mean free path —
  transition to kinetic regime along stochastic field lines.
- **Transport barrier (H-mode pedestal)**: the transport coefficients
  change by orders of magnitude across the edge transport barrier.
  The Braginskii coefficients are valid, but the turbulent contribution
  is suppressed (E×B shear decorrelation). The edge bootstrap current
  and its off-diagonal (Nernst, Ettingshausen) terms become critical
  for the radial electric field well E_r, which provides the shear
  suppression. Use neoclassical + turbulence saturation models (e.g.,
  QuaLiKiz, TGLF) that capture E×B shear quenching.
- **Gyrokinetic validity breaks down** when ρ* is not small (spherical
  tokamaks, edge) or when k_⊥ ρ_i ∼ 1 (full Larmor radius needed).
  Use full-orbit (PIC, Vlasov) when the gyrokinetic ordering fails;
  in practice, this occurs for energetic particles (fast ion orbits
  comparable to machine size) and for edge turbulence with large blobs.

## Cross-References

- Chen §5, Wesson §3, Braginskii (1965), Handbook of Plasma Physics Part 1 (Rosenbluth & Sagdeev, eds.) Vol.1 §2
- landau-graph: reasoning.kinetic_equation_closure (moments + closure → transport)
- plasma: reasoning.plasma.single_particle_drifts (GC drift velocities feed into
  Braginskii flux calculations; transport coefficients are the FLUID averaging of
  single-particle drifts — bidirectional)
