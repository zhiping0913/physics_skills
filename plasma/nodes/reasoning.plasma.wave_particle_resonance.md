---
skill_id: reasoning.plasma.wave_particle_resonance
type: reasoning
summary_50t: >
  ω−k_∥v_∥ = nω_c selects resonant particles that stay in phase with wave.
  n=0: Landau damping (electrostatic) + transit-time (magnetic). n=±1: cyclotron.
  |n|≥2: Bernstein (undamped). Quasilinear diffusion: ∂f₀/∂t = ∂/∂v(D_QL ∂f₀/∂v).
trigger:
  - computing wave damping/growth from particle distribution
  - need resonant velocity condition for specific harmonic
  - quasilinear evolution of distribution function
reasoning_role: resonance_condition
parent: reasoning.landau_damping
retrieval_cost: 1
references:
  - landau-graph: reasoning.landau_damping (n=0 electrostatic case)
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

## Derivation Sketch (from Landau damping → general resonance)

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

4. **Quasilinear plateau formation** (nonlinear saturation): the wave spectrum
   diffuses resonant particles in velocity space along diffusion paths
   v_⊥² + (v_∥ − ω/k_∥)² = const. Particles diffuse until ∂f₀/∂v along
   the diffusion path vanishes — a PLATEAU forms. The plateau is the
   maximum-entropy state for the resonant population; the wave growth
   saturates when the free energy (positive slope) is exhausted.

5. **H-theorem connection**: the quasilinear diffusion operator is a
   Fokker-Planck operator ∂f₀/∂t = ∂/∂v·(D_QL·∂f₀/∂v), where D_QL
   is positive-definite. This implies dS/dt ≥ 0 for the kinetic entropy
   S = −∫ f₀ ln f₀ dv — the resonant wave-particle interaction irreversibly
   increases entropy, converting ordered wave energy into thermal spread
   of the distribution. This is the microscopic basis for the second law
   in collisionless plasmas: Landau damping IS entropy production.

## Algorithm

```
1. Write wave fields in particle's guiding-center frame:
   E(t) = Σ E_n exp[i(k_∥ z_∥ + k_⊥ r_L sin θ − ωt)]

2. Expand in Bessel functions: exp(ik_⊥ r_L sin θ) = Σ J_m(k_⊥ r_L) e^{imθ}

3. The particle sees frequency-shifted components at ω' = ω − k_∥ v_∥ − m ω_c.
   Resonance: ω' = 0 → ω − k_∥ v_∥ = n ω_c.

4. Resonant particles EXCHANGE energy with the wave:
   - ∂f₀/∂v|_{v_res} < 0 → LANDAU DAMPING (energy from wave to particles)
   - ∂f₀/∂v|_{v_res} > 0 → INVERSE DAMPING / INSTABILITY (bump-on-tail)

5. For n=0 (Landau, transit-time): parallel dynamics, no B₀ needed.
   For n=±1 (cyclotron): perpendicular dynamics, needs B₀.
   For |n|≥2 (Bernstein): finite Larmor radius, K⊥ρ_L ∼ n, undamped.
```

## Resonance Types

| n | Name | Physics | Damping mechanism |
|---|------|---------|-------------------|
| 0 | Landau | Electrostatic, E_∥ | Parallel trapping, phase mixing |
| 0 | Transit-time | Magnetic, μ∇B force | Mirror force on magnetic moment |
| ±1 | Cyclotron | E_⊥ rotates with particle | Perpendicular heating |
| ±2,... | Bernstein | Finite Larmor radius | Undamped! (k_∥ → 0) |

## Quasilinear Theory (Stix §10, Chen §8)

Beyond linear damping: the wave spectrum modifies f₀(v) via diffusion:

```
∂f₀/∂t = ∂/∂v_∥ (D_∥ ∂f₀/∂v_∥) + (1/v_⊥)∂/∂v_⊥ (v_⊥ D_⊥ ∂f₀/∂v_⊥)
D ∝ Σ |E_k|² δ(ω_k − k_∥ v_∥ − n ω_c)
```

This flattens f₀ near resonance → saturation of instability → plateau formation.

**Plateau formation — explicit**: for 1D electrostatic (Langmuir), the
diffusion path is v_∥ only. Initial positive slope ∂f₀/∂v_∥ > 0 drives
wave growth; quasilinear diffusion fills the "valley" between the bulk
and the bump until ∂f₀/∂v_∥ = 0 on the interval v_bulk ≤ v_∥ ≤ v_bump.
The resonant interval widens until the plateau covers all unstable phase
velocities. Total energy: W_wave + ∫ ½ m v² f₀(v) dv = const (Manley-Rowe).
**H-theorem**: dS/dt = −∫ (∂f₀/∂v)·D_QL·(∂f₀/∂v) dv / f₀ ≥ 0,
since D_QL is positive-definite. Equality only at plateau (∂f₀/∂v = 0
on resonance).

### Nonlinear Landau Damping, BGK Modes, and Plasma Echoes

**Nonlinear Landau damping**: when two waves (ω₁,k₁) and (ω₂,k₂) beat
to produce a virtual wave at (ω₁±ω₂, k₁±k₂) that resonantly interacts
with particles, transferring energy BETWEEN waves without net particle
heating. Rate ∝ |E₁|² |E₂|². Important for saturation of parametric
instabilities and for spectral energy transfer in turbulence.

**BGK (Bernstein-Greene-Kruskal) modes**: exact nonlinear Vlasov-Poisson
equilibria where trapped particles in the wave potential well maintain
an undamped, finite-amplitude wave. The distribution function is
f(v) = f(E) where E = ½ mv² − eφ is the total energy in the wave frame.
ANY such f(E) satisfies the steady Vlasov equation. These are the
nonlinear endpoint of Landau damping — the wave does NOT decay to zero
but to a BGK mode of finite amplitude. The final amplitude depends on
the initial wave energy and the number of trapped particles.

**Plasma echoes**: a remarkable nonlinear effect demonstrating the
REVERSIBILITY of the Vlasov equation. Two pulses separated by time τ
produce an echo at time 2τ (temporal echo) or position 2k₁−k₂ (spatial
echo). The echo arises because phase-mixing (Landau damping) stores
information in fine-scale velocity-space structure, which a second
pulse can "unmix." The echo amplitude decays as exp(−const × γ_L τ)
where γ_L is the Landau damping rate — the stored information leaks
away via phase-space diffusion (collisions, nonlinear broadening).
Echoes prove that Landau damping is NOT true irreversibility in the
collisionless limit — it's phase mixing, which is reversible in
principle but practically irreversible due to coarse-graining.

## Edge Cases

- **k_⊥ ρ_L → 0 (cold limit)**: J_n(k_⊥ ρ_L) → 0 for all |n| ≥ 1.
  Only n=0 resonance survives — the particle responds only to E_∥
  (Landau) and the mirror force (transit-time). All cyclotron and
  Bernstein harmonics vanish. This is the cold plasma regime.
  Breaks down when k_⊥ ρ_L > 0.1 — use the full Bessel expansion
  with at least |n| ≤ k_⊥ ρ_L + 3 harmonics.
- **k_∥ → 0 (purely perpendicular propagation)**: the Landau resonance
  condition ω − k_∥ v_∥ = n ω_c collapses to ω = n ω_c. ALL particles
  with the same n are resonant regardless of v_∥ → no phase mixing →
  NO Landau damping (n=0) or cyclotron damping (n=±1). This is why
  Bernstein waves (k_∥=0) are undamped. Breaks down when thermal
  broadening via ω_D (magnetic drift) or collisions provide a small
  effective k_∥ — damping is weak but nonzero.
- **Nonlinear regime (wave amplitude large)**: when the bounce frequency
  ω_B = √(e k² φ/m) of trapped particles exceeds the Landau damping
  rate γ_L (i.e., ω_B > γ_L), linear theory fails. Particles bounce in
  the wave potential faster than the wave damps → nonlinear saturation
  via trapping. The O'Neil (1965) solution shows that the wave amplitude
  oscillates and eventually settles to a constant (BGK) value. Use
  Vlasov simulation (or BGK theory) when eφ/T_e > (γ_L/ω_p)²; linear
  Landau formula overestimates damping in this regime.
- **Relativistic resonance**: when v_res ∼ c, the non-relativistic
  resonance condition ω − k_∥ v_∥ = n ω_c/γ fails. The correct
  relativistic resonance is ω − k_∥ v_∥ = n ω_c/γ, where γ = 1/√(1−v²/c²)
  and ω_c includes the relativistic mass increase. This is critical for
  ECRH (electron cyclotron resonance heating) at T_e > 50 keV and for
  runaway electron interaction with waves. The resonance curve in (v_∥, v_⊥)
  space becomes an ellipse, not a line. Use fully relativistic dispersion
  with the relativistic plasma dispersion function when T_e > 50 keV.
- **Multiple overlapping resonances**: when |n₁ ω_c₁ − n₂ ω_c₂| < γ_L
  for two species, resonances overlap and the quasilinear diffusion
  paths can connect different regions of phase space. This can lead to
  enhanced transport (synergistic heating) or mode conversion. Use
  multi-species kinetic codes (AORSA, TORIC) when ion and electron
  cyclotron harmonics overlap. In the extreme limit, resonance overlap
  produces stochastic heating (Chirikov criterion for resonance overlap).

## Cross-References

- Stix §8-10, Chen §7-8, Ginzburg §6-7
- landau-graph: reasoning.landau_damping (n=0 electrostatic)
- landau-graph: reasoning.plasma_dielectric_response (ε_l from Vlasov)
