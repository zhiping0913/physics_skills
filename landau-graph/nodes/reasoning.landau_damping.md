---
skill_id: reasoning.landau_damping
type: reasoning
summary_50t: >
  Vlasov-Poisson + analytic continuation (ω→ω+i0) → Im ε_l ≠ 0 → damping.
  Collisionless damping! Energy transfers from wave to resonant particles
  with v ≈ ω/k. Pole prescription from causality (adiabatic turn-on).
trigger:
  - collisionless plasma wave
  - ω/k near thermal velocity
  - need to determine damping rate without collisions
reasoning_role: collisionless_dissipation
parent: reasoning.kinetic_equation_closure
children:
  - knowledge.kinetic.plasma_dielectric
  - knowledge.kinetic.landau_damping_formula
retrieval_cost: 1
---

# reasoning.landau_damping — Vlasov Equation → Collisionless Damping

## Core Picture

A plasma wave (e.g., Langmuir oscillation) has ω ≈ ω_p for k→0.
But the Vlasov equation reveals: even without collisions, the wave DAMPS.

Why? Particles with v ≈ ω/k are in resonance with the wave. Those moving
slightly slower than the wave gain energy from it (damping). Those moving
slightly faster lose energy (driving). For a Maxwellian distribution, there
are more slower particles → net damping.

The mathematics: the Vlasov-Poisson integral has a pole at v = ω/k.
The physically correct prescription is ω → ω + i0 (Landau's rule).
This gives Im ε_l ≠ 0 → dissipation without collisions.

## Algorithm

```
1. Linearize Vlasov: f = f_0 + δf, δf ∝ e^{i(kx−ωt)}
2. δf = (eE/i(kv−ω)) ∂f_0/∂p
3. Compute charge density: ρ = −e∫δf d³p
4. Poisson: ikE = 4πρ → ε_l(k,ω) = 1 − (4πe²/k²)∫(k·∂f_0/∂p)/(kv−ω−i0) d³p
5. Landau's rule ω→ω+i0: causality (field turned on at t=−∞) 
   or equivalently: collisions → 0 limit (ν→0)
6. Im ε_l = −(4π²e²m/k²)[df_0(p_x)/dp_x] at v_x = ω/k
7. For Maxwellian: Im ε_l ∝ exp(−ω²/2k²v_T²) → exponential damping at ω/kv_T ≫ 1
8. Damping rate: γ = −Im ε_l/(∂Re ε_l/∂ω)
```

## Landau's Pole Prescription

```
1/(kv−ω−i0) = P(1/(kv−ω)) + iπ δ(kv−ω)
```
The δ-function selects resonant particles. The principal value gives
the reactive (dispersive) part. The δ-function gives dissipation.

This is a GENERAL technique for kinetic equations: analytic continuation
of integrals with resonant denominators. Applies whenever a wave interacts
with a continuous spectrum of particles.

## Key Insight

**Order of limits matters**. Landau's derivation involves two limits:
(1) small field (linearization), (2) ν→0 (collisionless). They DO NOT COMMUTE:
you must linearize FIRST, then take ν→0. If you take the collisionless limit
first, δf would diverge at resonance (kv=ω), and linearization would fail
because δf would not be small compared to f₀. This is why the Landau prescription
ω→ω+i0 must be introduced — it regularizes the resonance while preserving
the physical content of the collisionless limit.

**Thermodynamic reversibility**: Collisionless dissipation does NOT involve
entropy increase. It is thermodynamically REVERSIBLE — information is not lost,
it is transferred to fine-grained structure in f(v). This is confirmed by
plasma echo experiments (§35): a second pulse can recover the damped wave.

## Edge Cases

- ω/kv_T ≫ 1: damping exponentially small (few resonant particles)
- ω/kv_T ~ 1: strong damping (many resonant particles) — wave not a normal mode
- Non-Maxwellian f_0: can have INVERSE Landau damping (instability) if df_0/dv > 0

## Cross-References
- Landau Vol.10 §29-30 (Landau damping), §35 (plasma echo)
- Landau Vol.10 §61 (beam instability — inverse Landau damping)
- Landau Vol.1 §49 (adiabatic turn-on → i0 prescription)
