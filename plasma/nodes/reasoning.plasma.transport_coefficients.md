---
skill_id: reasoning.plasma.transport_coefficients
type: reasoning
summary_50t: >
  Collisions → transport. Magnetized: χ⊥≪χ∥ (∝B₀⁻²). Classical (Braginskii,
  Chapman-Enskog for plasma) → neoclassical (banana/plateau/Pfirsch-Schlüter,
  Galeev-Sagdeev) → anomalous (turbulent, quasilinear). Bootstrap current
  from ∇p in toroidal geometry. Scaling: τ_E ∼ I_p P^{−α}.
trigger:
  - computing heat/particle/momentum transport in magnetized plasma
  - understanding confinement scaling for fusion
  - distinguishing classical/neoclassical/anomalous transport contributions
reasoning_role: transport
parent: reasoning.kinetic_equation_closure
retrieval_cost: 1
references:
  - landau-graph: reasoning.kinetic_equation_closure
  - Вопросы теории плазмы: Vol.1 (классический перенос), Vol.4 (уравнения переноса), Vol.7 (неоклассика, Галеев-Сагдеев), Vol.16 (тороидальный перенос)
  - Braginskii, Handbook of Plasma Physics Part 1; Chen §5; Wesson §3
---

# reasoning.plasma.transport_coefficients — Collisions → Confinement

## Core Picture

In magnetized plasma, transport ACROSS B₀ is suppressed by the magnetic field,
but enhanced by toroidal geometry and dominated by turbulence. Three transport
regimes form a nested hierarchy: **classical** (collisional, straight B₀) →
**neoclassical** (collisional, toroidal B₀) → **anomalous** (turbulent, always
dominant in fusion plasmas). Each regime has a characteristic scaling with
collisionality, magnetic geometry, and driving gradients. The Soviet school's
Вопросы теории плазмы (Vol.1,4,7,16) provided the foundational derivations for
both classical (Chapman-Enskog adaptation, Vol.1) and neoclassical (banana-
plateau-Pfirsch-Schlüter, Galeev-Sagdeev, Vol.7,16) transport.

## Derivation Sketch (from kinetic closure → transport tensors)

Starting from `landau-graph: reasoning.kinetic_equation_closure` (which
establishes that kinetic equations truncated at finite moments require
closure relations — the stress tensor Π and heat flux q), the transport
coefficients are the CLOSURE OUTPUTS. The derivation follows a three-level
hierarchy, each refining the previous:

### 1. Classical transport — Braginskii (from Chapman-Enskog)

The method originates in the kinetic theory of neutral gases (Chapman-Enskog)
and was adapted to fully ionized plasma in Вопросы теории плазмы Vol.1 (1963)
and later systematized by Braginskii (Handbook of Plasma Physics Part 1).

**Key differences from neutral-gas Chapman-Enskog** (VTP Vol.1):
- The collision integral uses the **Landau (Fokker-Planck)** form, not
  Boltzmann — Coulomb collisions are dominated by cumulative small-angle
  scattering rather than large-angle binary encounters.
- Electron and ion distributions are **coupled through the friction force**
  R = −∫ m_e v C_{ei}(f_e, f_i) d³v, producing the thermoelectric effects
  (Nernst, Ettingshausen) absent in neutral gases.
- The magnetic field introduces a **preferred direction** — transport splits
  into ∥, ⊥, and ∧ (Hall) components.

**Braginskii's procedure**: expand f = f_M + f_1, solve the linearized kinetic
equation with the Landau collision operator, compute the fluxes in terms of
thermodynamic forces (∇n_α, ∇T_α, E* = E + v_α×B, R_αβ). The resulting
transport matrix for each species:

```
Γ_α = −D_α·∇n_α − n_α μ_α·E* − n_α δ_α·∇T_α
q_α = −κ_α·∇T_α − n_α T_α φ_α·E* − T_α ν_α·∇n_α
```

where each coefficient (D, μ, δ, κ, φ, ν) is a tensor with components
parallel (∥), perpendicular (⊥), and cross (∧, Hall) to B₀.

**Key transport coefficients** (magnetized, two-fluid):

```
η_∥ = m_e ν_ei / (n e²)                         [Spitzer resistivity]
χ_e∥ ≈ 3.2 n_e T_e / (m_e ν_ei)                 [parallel electron thermal conduct.]
χ_e⊥ = χ_e∥ / (1 + ω_ce²/ν_ei²)                 [⊥ suppressed by magnetization]
D_⊥ = η_∥ n T / B₀²                              [classical particle diffusion]
```

**Magnetic suppression**: χ⊥/χ∥ ∼ 1/(Ω_e τ_ei)² ∼ (ρ_e/λ_mfp)² ≪ 1. This
is why fusion plasmas can reach 10⁸ K while the walls remain cool — heat
transport across B₀ is suppressed by 10⁸–10¹⁰ relative to ∥.

**Thermo-electric (off-diagonal) coefficients** — arise from unlike-species
coupling in the collision operator (VTP Vol.1):
- **Ettingshausen effect**: heat flux driven by electric field (φ term)
- **Nernst effect**: electric field from ∇T (δ, ν terms)
- **Thermo-power**: V_th = −∫ (δ_∥/σ_∥) ∇_∥ T_e · dl (Seebeck for plasma)

**Full Braginskii transport matrix**:

| Flux | ∥ component | ⊥ component | ∧ (Hall) component |
|------|------------|------------|-------------------|
| Γ (particle) | −D_∥ ∇_∥ n | −D_⊥ ∇_⊥ n + D_∧ (ĥ×∇n) | E×B / curvature |
| q (heat) | −κ_∥ ∇_∥ T | −κ_⊥ ∇_⊥ T + κ_∧ (ĥ×∇T) | Righi-Leduc |
| Π (stress) | η₀ W_∥ | η₁ W_⊥ | η₂ (gyroviscosity) |

These off-diagonal terms dominate in the pedestal and divertor where ∇T is
large and MHD equilibrium enforces specific current patterns.

### 2. Neoclassical transport — Galeev-Sagdeev (VTP Vol.7, 1973)

Classical transport assumes straight, uniform B₀. In toroidal geometry, the
1/R variation of |B| creates magnetic mirrors that TRAP particles on the
outboard side. Trapped particles execute "banana" orbits with width Δ_b ≫ ρ_i,
enhancing transport far beyond the classical level. This was THE seminal
contribution of the Soviet school (Galeev & Sagdeev, VTP Vol.7, 1973; further
developed in Vol.16, 1987).

**Trapped particle fraction**: f_t ≈ √(2ε) where ε = r/R₀ is the inverse
aspect ratio. For a typical tokamak (ε ∼ 0.3): ∼80% of particles are trapped.

**Collisionality parameter** (VTP Vol.7):
```
ν* = ν_eff / ω_bounce,    ω_bounce ≈ (ε/2)^{1/2} v_th / (q R₀)
```
Three regimes defined by ν*:

| Regime | ν* | χ scaling | Physics |
|--------|-----|-----------|---------|
| **Banana** (Galeev-Sagdeev) | ν* ≪ 1 | q² ε^{−3/2} ν_ei ρ_i² | Trapped particles complete full banana orbits between collisions |
| **Plateau** | ν* ∼ 1 | ε^{1/2} v_th²/(Ω_i R) | Resonant detrapping at ν_eff ∼ ω_bounce |
| **Pfirsch-Schlüter** | ν* ≫ 1 | q² ν_ei ρ_i² | Collisional — helical field gives 1/ε enhancement over classical |

**Banana regime formula** (most relevant for fusion-reactor conditions):
```
χ_i^neo ≈ q² ε^{−3/2} ν_ii ρ_i²    [ion neoclassical thermal diffusivity]
```
ε = r/R₀, q = safety factor. For ITER-like parameters: χ_i^neo / χ_i^classical ∼ 10–100.

**Bootstrap current** (VTP Vol.7): the ∇p-driven trapped-particle orbits
produce a toroidal current WITHOUT an external loop voltage:
```
j_BS ≈ √ε (T / B_θ) dp/dr
```
This current is essential for steady-state tokamak operation — it can provide
50–90% of the total plasma current, dramatically reducing the required
external current drive power.

The VTP Vol.4 (1964) provided the transport equation formalism (moments of
the kinetic equation with closure assumptions) that underlies both the
classical Braginskii treatment and the neoclassical generalization.

### 3. Anomalous (turbulent) transport — quasilinear closure

Even neoclassical transport is far too small to explain experimental
confinement — the observed χ_eff is typically 10²–10⁴ × larger. This is
**anomalous transport**, driven by microturbulence.

**Quasilinear theory** (Vedenov 1963, VTP Vol.6; developed further in Vol.7):
the turbulent E×B fluctuations produce a radial particle flux:
```
Γ = ⟨ñ ṽ_E⟩,    D_anom ≈ Σ_k (k_θ/k_∥)² |eφ_k/T|² (cT/eB)
```
The quasilinear diffusion coefficient D_QL ∝ Σ_k |E_k|² δ(ω_k − k·v) is
proportional to the spectral energy density of unstable waves. Saturation
occurs when quasilinear flattening of ∂f₀/∂v removes the free energy source.

**Gyrokinetic procedure** (modern computational approach):
1. Compute axisymmetric equilibrium (Grad-Shafranov → flux surfaces)
2. Linear gyrokinetic analysis (GS2, GENE, GYRO): unstable modes (ITG, TEM, ETG, KBM)
3. Nonlinear gyrokinetic simulation: evolve δf until saturated turbulence
4. Compute fluxes: Γ = ⟨δn δv_E⟩, Q = ⟨δp δv_E⟩ as time averages

**Mixing-length estimate**: D_turb ∼ γ/k_⊥² where γ, k_⊥ are from the dominant
microinstability. Empirical confinement scaling: τ_E ∝ I_p^α P^{−β} n^{γ}
(e.g., IPB98(y,2)).

## Algorithm — Given (T, n, B₀, geometry) → Transport Regime

```
1. COMPUTE collisionality: ν_ei, ν_ii from Coulomb logarithm.
   ν* = ν_eff / ω_bounce (for toroidal geometry).

2. CLASSICAL: compute Braginskii coefficients.
   χ_class ∝ 1/(Ω_e τ_ei)² χ_∥. Always a lower bound.

3. NEOCLASSICAL: if toroidal, compute ν* → banana/plateau/PS regime.
   Banana: χ_neo ≈ q² ε^{−3/2} ν_ii ρ_i².
   Bootstrap: j_BS ≈ √ε (T/B_θ) dp/dr.

4. ANOMALOUS: dominant in all fusion plasmas.
   Mixing-length: D_turb ∼ γ/k_⊥² from ITG/TEM/ETG.
   Quasilinear: D_QL ∝ Σ_k |φ_k|².

5. TOTAL: χ_eff = χ_neo + χ_anom (χ_class negligible in toroidal geometry).
   Compare with experimental power-balance.
```

## Edge Cases

- **Collisionless limit (ν* → 0)**: the Chapman-Enskog/Braginskii expansion
  assumes small mean free path. When ν_ei → 0, fluid closure fails — use
  collisionless Vlasov with Landau damping. In practice, ion-scale Braginskii
  holds even in "collisionless" fusion plasmas, but electron ∥ transport at
  high T_e may need kinetic treatment (Spitzer-Härm with e-e collisions
  converged, or nonlocal when λ_ei > L_T).
- **Nonlocal transport (λ_mfp > L_T)**: in ICF hot spots and tokamak edges,
  the local Fourier law q = −κ∇T fails. The VTP formalism (kinetic rather
  than fluid) provides the foundation for nonlocal models — the flux at a
  point depends on the temperature profile over λ_mfp. Use SNB or Vlasov-
  Fokker-Planck (VFP) codes. Signature: preheat ahead of the conduction
  front that Fourier models miss.
- **Stochastic magnetic fields**: when islands overlap (Chirikov criterion),
  parallel transport along tangled field lines dominates: χ_eff ∼ D_M χ_∥.
- **Transport barrier (H-mode pedestal)**: E×B shear suppresses turbulence,
  reducing χ_eff to near-neoclassical. Bootstrap current and off-diagonal
  (Nernst, Ettingshausen) terms critical for E_r well formation.
- **VTP Vol.15 (1987) — high-β transport**: in plasmas with β ≳ 1, magnetic
  field is significantly modified by the plasma pressure. The transport
  coefficients become functions of β, and magnetic field generation
  (dynamo effects) couples back to the transport — a regime not covered
  by standard Braginskii or neoclassical theory.

## Cross-References

- Braginskii, Handbook of Plasma Physics Part 1; Chen §5; Wesson §3
- Вопросы теории плазмы: Vol.1 (1963) — classical Chapman-Enskog for plasma, Vol.4 (1964) — transport equations, Vol.6 (1972) — quasilinear effects, Vol.7 (1973) — neoclassical Galeev-Sagdeev, Vol.16 (1987) — toroidal transport
- landau-graph: reasoning.kinetic_equation_closure (moments + closure → transport)
- plasma: reasoning.plasma.single_particle_drifts (GC drift velocities feed Braginskii fluxes)
- plasma: reasoning.plasma.wave_particle_resonance (quasilinear diffusion theory)
