---
skill_id: reasoning.plasma.wave_particle_resonance
type: reasoning
summary_50t: >
  ω−k_∥v_∥ = nω_c selects resonant particles that stay in phase with wave.
  n=0: Landau damping (electrostatic) + transit-time (magnetic). n=±1: cyclotron.
  |n|≥2: Bernstein (undamped). Quasilinear diffusion: ∂f₀/∂t = ∂/∂v(D_QL ∂f₀/∂v)
  with D_QL ∝ Σ_k |E_k|² (Vedenov 1963). Anomalous transport from turbulent
  E×B fluctuations. Transition to strong turbulence (Zakharov).
trigger:
  - computing wave damping/growth from particle distribution
  - need resonant velocity condition for specific harmonic
  - quasilinear evolution of distribution function
  - estimating anomalous transport from turbulence spectra
reasoning_role: resonance_condition
parent: reasoning.landau_damping
retrieval_cost: 1
references:
  - landau-graph: reasoning.landau_damping (n=0 electrostatic case)
  - Вопросы теории плазмы: Vol.6 (1972) — Веденов, Рютов, квазилинейные эффекты; Vol.7 (1973) — нелинейные кинетические неустойчивости, аномальный перенос
---

# reasoning.plasma.wave_particle_resonance — Phase Matching → Energy Exchange

## Core Picture

Wave-particle interaction occurs when a particle sees a STATIONARY wave phase
in its own reference frame. The general resonance condition for a magnetized
plasma (Stix §8-9, Chen §7, Ginzburg §6):

```
ω − k_∥ v_∥ = n ω_c    (n = 0, ±1, ±2, ...)
```

where ω_c = qB₀/m is the (signed) cyclotron frequency. Each n selects a
different harmonic of the cyclotron motion.

When many resonant waves are present, the cumulative effect is described by
**quasilinear theory** — the resonant particles diffuse in velocity space,
flattening the distribution function and producing anomalous transport. This
theory was developed extensively in the Soviet school (Vedenov, Ryutov —
Вопросы теории плазмы Vol.6, 1972; Galeev, Sagdeev — Vol.7, 1973).

## Derivation Sketch (from Landau damping → general resonance → quasilinear)

Starting from `landau-graph: reasoning.landau_damping` (which establishes
the n=0 electrostatic resonance — a particle resonant when its parallel
velocity matches the wave phase velocity, v_∥ = ω/k_∥), the magnetized
generalization adds cyclotron sidebands:

1. **Guiding-center frame decomposition**: in a magnetized plasma, the
   particle orbit is z(t) = z₀ + v_∥ t + r_L sin(ω_c t + φ), with
   r_L = v_⊥/|ω_c|. The wave electric field at the particle position:
   E(t) = Σ E_n exp[i(k_∥z₀ + k_∥v_∥t + k_⊥r_L sin(ω_c t + φ) − ωt)].

2. **Bessel-function expansion** (the key step): exp(ik_⊥ r_L sin θ) =
   Σ_{m=−∞}^{∞} J_m(k_⊥ r_L) e^{imθ}. Substituting, the particle sees
   frequency-shifted components at ω' = ω − k_∥ v_∥ − m ω_c.
   Resonance occurs when ω' = 0 for some m. KEY NON-OBVIOUS: the
   coupling strength for harmonic n is proportional to J_n(k_⊥ ρ_L)²,
   meaning high-n harmonics require finite Larmor radius (k_⊥ ρ_L ∼ n).

3. **From resonance to energy exchange**: the power transfer is
   P = q ⟨v·E⟩ = −(q²/2m) Σ_n |E_{n,eff}|² Im[∫ dv f₀(v)/(ω − k_∥v_∥ − nω_c)].
   For n=0 (Landau): damping is proportional to ∂f₀/∂v_∥ at v_∥=ω/k_∥.
   For n=±1 (cyclotron): damping proportional to (v_⊥/2) ∂f₀/∂v_⊥ +
   v_res ∂f₀/∂v_∥ — perpendicular AND parallel gradients both contribute.

## Quasilinear Theory — Vedenov Formalism (VTP Vol.6, 1972)

When MANY unstable waves are present simultaneously, the resonant particles
experience a net diffusive evolution in velocity space. The quasilinear
theory, developed by Vedenov, Velikhov, and Sagdeev (1962-63) and
systematized in Вопросы теории плазмы Vol.6 (Vedenov & Ryutov, 1972),
provides the self-consistent coupling between the wave spectrum and the
slowly-evolving particle distribution.

### 1. Quasilinear diffusion equation (Vedenov 1963)

The resonant particles evolve via a Fokker-Planck-type diffusion:

```
∂f₀/∂t = ∂/∂v · (D_QL · ∂f₀/∂v)
D_QL(v) = (πq²/m²) Σ_k |E_k|² δ(ω_k − k·v)    [unmagnetized]
D_QL(v) = (πq²/m²) Σ_{k,n} |E_{k,n}|² J_n²(k_⊥ρ_L) δ(ω_k − k_∥v_∥ − nω_c)  [magnetized]
```

The diffusion coefficient D_QL is proportional to the spectral energy
density of the waves at the resonant velocity. This is the central result:
the wave spectrum |E_k|² acts as a "collision operator" for the resonant
particles.

**Diffusion paths** (VTP Vol.6): in magnetized plasma, particles diffuse
along curves in (v_∥, v_⊥) space where the resonance condition holds:
v_⊥² − (ω_k/k_∥)(v_∥ − ω_k/k_∥)² / ω_c = const. These paths connect
different regions of phase space, enabling cross-heating between ∥ and ⊥
degrees of freedom.

### 2. Saturation by plateau formation

The quasilinear diffusion acts to FLATTEN the distribution function along
the resonant diffusion paths. For 1D electrostatic Langmuir waves:

```
∂f₀/∂t = ∂/∂v (D_QL ∂f₀/∂v)    with D_QL ∝ |E_k|² at k = ω_p/v
```

An initial positive slope ∂f₀/∂v > 0 (bump-on-tail) drives wave growth.
The growing waves increase D_QL, which flattens f₀ near the resonant
velocity. When ∂f₀/∂v = 0 (plateau formed), growth stops — the free
energy source is exhausted. The saturated wave energy density is:

```
∫ |E_k|² dk / 8π = ∫_{v_min}^{v_max} ½ m n_bump (v − v_avg)² dv
```

— the initial excess kinetic energy of the bump is transferred to the waves.

**H-theorem** (VTP Vol.6): the quasilinear operator is positive-definite,
so dS/dt = −∫ (∂f₀/∂v)·D_QL·(∂f₀/∂v) dv / f₀ ≥ 0. Entropy increases
irreversibly — Landau damping IS entropy production in collisionless plasma.

### 3. Anomalous transport from turbulence (VTP Vol.7, 1973)

In magnetized plasma, the turbulent E×B drift produces a radial particle flux:

```
Γ_r = ⟨ñ ṽ_E·r̂⟩ = Σ_k (k_θ/B) Im⟨ñ* φ_k⟩
```

In the quasilinear approximation (VTP Vol.7, Galeev & Sagdeev):

```
D_anom ≈ Σ_k (k_θ/k_∥)² |eφ_k/T|² (cT/eB)    [Fick's law: Γ = −D_anom ∇n]
```

This is the **anomalous transport** that dominates all tokamaks:
D_anom / D_neo ∼ 10²–10⁴. The physical mechanism: E×B convection of
particles by turbulent eddies produces a net radial flux when the
fluctuations are correlated with density perturbations.

### 4. Transition to strong turbulence (VTP Vol.7)

The quasilinear theory assumes RANDOM PHASES among the waves — a weak
turbulence condition. This breaks down when:

```
ω_B > γ_L    where ω_B = √(e k² φ / m) is the bounce frequency
```

When particles are trapped in the wave potential faster than the wave
grows/damps, phase correlations become important. The system transitions
to **strong turbulence**, described by the Zakharov equations (see
`em.positive_feedback_instability`). In this regime, self-organized
structures (solitons, collapse cavities, phase-space holes) replace
the random-phase wave ensemble.

## Resonance Types

| n | Name | Physics | Damping mechanism |
|---|------|---------|-------------------|
| 0 | Landau | Electrostatic, E_∥ | Parallel trapping, phase mixing |
| 0 | Transit-time | Magnetic, μ∇B force | Mirror force on magnetic moment |
| ±1 | Cyclotron | E_⊥ rotates with particle | Perpendicular heating |
| ±2,... | Bernstein | Finite Larmor radius | Undamped! (k_∥ → 0) |

## Algorithm

```
1. Write wave fields in particle's guiding-center frame:
   E(t) = Σ E_n exp[i(k_∥ z_∥ + k_⊥ r_L sin θ − ωt)]

2. Expand in Bessel functions: exp(ik_⊥ r_L sin θ) = Σ J_m(k_⊥ r_L) e^{imθ}

3. The particle sees frequency-shifted components at ω' = ω − k_∥ v_∥ − m ω_c.
   Resonance: ω' = 0 → ω − k_∥ v_∥ = n ω_c.

4. Resonant particles EXCHANGE energy with the wave:
   - ∂f₀/∂v|_{v_res} < 0 → LANDAU DAMPING
   - ∂f₀/∂v|_{v_res} > 0 → INVERSE DAMPING / INSTABILITY

5. WAVE SPECTRUM: for quasilinear evolution (multiple waves):
   D_QL ∝ Σ_k |E_k|² δ(ω_k − k_∥ v_∥ − n ω_c)
   ∂f₀/∂t = ∂/∂v (D_QL ∂f₀/∂v) → plateau formation → saturation.

6. ANOMALOUS FLUX: Γ = ⟨ñ ṽ_E⟩ ≈ −D_anom ∇n, with D_anom from Step 5.
```

### Nonlinear Landau Damping, BGK Modes, and Plasma Echoes

**Nonlinear Landau damping**: when two waves (ω₁,k₁) and (ω₂,k₂) beat
to produce a virtual wave at (ω₁±ω₂, k₁±k₂) that resonantly interacts
with particles, transferring energy BETWEEN waves without net particle
heating. Rate ∝ |E₁|² |E₂|². Important for saturation of parametric
instabilities and for spectral energy transfer in turbulence.

**BGK (Bernstein-Greene-Kruskal) modes**: exact nonlinear Vlasov-Poisson
equilibria where trapped particles in the wave potential well maintain
an undamped, finite-amplitude wave. ANY distribution f(v) = f(½mv²−eφ)
satisfies the steady Vlasov equation. These are the nonlinear endpoint
of Landau damping — the wave does NOT decay to zero but to a BGK mode.

**Plasma echoes**: a remarkable nonlinear effect demonstrating the
REVERSIBILITY of the Vlasov equation. Two pulses separated by time τ
produce an echo at time 2τ. The echo arises because phase-mixing stores
information in fine-scale velocity-space structure, which a second pulse
can "unmix." Proves Landau damping is phase mixing, not true irreversibility.

## Edge Cases

- **k_⊥ ρ_L → 0 (cold limit)**: J_n(k_⊥ ρ_L) → 0 for |n| ≥ 1. Only n=0
  resonance survives. Breaks down when k_⊥ ρ_L > 0.1.
- **k_∥ → 0 (purely perpendicular propagation)**: the resonance collapses
  to ω = n ω_c. ALL particles with same n are resonant → NO phase mixing →
  NO Landau/cyclotron damping. Bernstein waves are undamped.
- **Nonlinear regime (ω_B > γ_L)**: linear and quasilinear theories fail.
  Particle trapping dominates. Use BGK theory or Vlasov simulation when
  eφ/T_e > (γ_L/ω_p)² (VTP Vol.7).
- **Relativistic resonance**: at T_e > 50 keV, use ω − k_∥ v_∥ = n ω_c/γ
  with γ = 1/√(1−v²/c²). The resonance curve becomes an ellipse.
- **Overlapping resonances**: when |n₁ω_c₁ − n₂ω_c₂| < γ_L, resonant
  diffusion paths merge → enhanced cross-heating. Chirikov overlap
  criterion for stochasticity.
- **Multiple ion species**: each species has its own ω_cα and resonant
  velocity. The quasilinear diffusion paths for different species can
  intersect → synergistic heating (VTP Vol.15, electron beam heating).

## Cross-References

- Stix §8-10, Chen §7-8, Ginzburg §6-7
- Вопросы теории плазмы: Vol.6 (1972) — Vedenov & Ryutov, quasilinear effects; Vol.7 (1973) — nonlinear kinetic instabilities, anomalous transport; Vol.15 (1987) — relativistic electron beam heating
- landau-graph: reasoning.landau_damping (n=0 electrostatic)
- electrodynamics: reasoning.em.positive_feedback_instability (strong turbulence transition)
- plasma: reasoning.plasma.transport_coefficients (anomalous transport manifestation)
