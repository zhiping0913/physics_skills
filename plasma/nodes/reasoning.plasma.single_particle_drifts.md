---
skill_id: reasoning.plasma.single_particle_drifts
type: reasoning
summary_50t: >
  m dv/dt = q(E+v×B). Uniform B: v = v_∥ + v_⟂ (cyclotron). Guiding-center
  drifts: E×B (v_E=E×B/B²), ∇B (v_∇B=μ∇B×B/qB²), curvature (v_c=mv_∥²/R_c),
  polarization (v_p=(m/qB²)dE/dt). Magnetic moment μ=mv_⟂²/2B conserved.
trigger: computing single-particle trajectories in EM fields, guiding-center motion
reasoning_role: particle_drifts
parent: reasoning.plasma.dispersion_relation_method
retrieval_cost: 1
---

# reasoning.plasma.single_particle_drifts — E, B → Guiding-Center Motion

## Core Picture

In a magnetized plasma, charged particles gyrate around field lines at ω_c.
When E, ∇B, or field curvature is present, the GUIDING CENTER drifts across
B₀. These drifts are the foundation of particle confinement, transport, and
instability theory (Chen §2, Gurnett & Bhattacharjee §2).

## Algorithm (Chen §2)

```
1. Equation: m dv/dt = q(E + v×B). Decompose v = v_∥ + v_⟂.

2. Uniform B (no E): circular motion at ω_c=qB/m, r_L=v_⟂/ω_c.
   Magnetic moment: μ = mv_⟂²/(2B) = const (first adiabatic invariant).

3. E×B DRIFT (uniform E⟂B):
   Transform to E×B frame: E'=0 → v_E = E×B/B².
   ALL particles drift at same velocity (charge-independent!).
   This is the fundamental MHD fluid velocity.

4. ∇B DRIFT (|∇B| ≪ B/r_L):
   v_∇B = ±½v_⟂ r_L (B×∇B)/B² = (μ/q)(B×∇B)/B².
   ± sign: ions and electrons drift in OPPOSITE directions → current!

5. CURVATURE DRIFT (field line curvature R_c, |R_c|≫r_L):
   v_c = (mv_∥²/qB²)(R_c×B)/R_c².
   Equivalent to centrifugal force F_cf = mv_∥² R̂_c/R_c in v_F = F×B/qB².

6. COMBINED ∇B + CURVATURE (vacuum field, ∇×B=0 in low-β):
   v_∇B+v_c = (m/qB³)(v_∥²+½v_⟂²) B×∇B.
   Causes CHARGE SEPARATION → electric fields → further drifts.

7. POLARIZATION DRIFT (time-varying E):
   v_p = (m/qB²) dE/dt. Ions dominate (mass ratio m_i/m_e ≫ 1).
   Polarization current is essential for low-frequency plasma response.
```

## Adiabatic Invariants

μ = mv_⟂²/2B (first, from gyration). J = ∮ v_∥ dl (second, from bounce).
Φ = ∫ B·dS (third, flux through drift orbit). All conserved for slow
variations. μ conservation → magnetic mirror: v_∥²=v²−2μB/m → trapped
when B > B₀ (loss cone in velocity space).

## Cross-References

- Chen §2, Gurnett & Bhattacharjee §2, Fitzpatrick §2
- landau-graph: reasoning.adiabatic_invariance (μ conservation)
- plasma: reasoning.plasma.transport_coefficients (drifts → transport)
