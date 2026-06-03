---
skill_id: reasoning.plasma.single_particle_drifts
type: reasoning
summary_50t: >
  m dv/dt = q(E+v×B). Uniform B: v = v_∥ + v_⟂ (cyclotron). Guiding-center
  drifts: E×B (v_E=E×B/B²), ∇B (v_∇B=μ∇B×B/qB²), curvature (v_c=mv_∥²/R_c),
  polarization (v_p=(m/qB²)dE/dt), gravity (v_g=(m/q)g×B/B²). μ=mv_⟂²/2B
  conserved as first adiabatic invariant.
trigger: computing single-particle trajectories in EM fields, guiding-center motion
reasoning_role: particle_drifts
parent: reasoning.plasma.dispersion_relation_method
retrieval_cost: 1
sign_convention: >
  Cyclotron frequency ω_c = |q|B/m (unsigned; often signed ω_c = qB/m with
  sign from q — ions positive, electrons negative). See electrodynamics:
  reasoning.plasma.dielectric_tensor_magnetized for signed convention in
  the dielectric tensor context. E×B drift is charge-independent; ∇B and
  curvature drifts have sign reversal for ions vs electrons.
---

# reasoning.plasma.single_particle_drifts — E, B → Guiding-Center Motion

## Core Picture

In a magnetized plasma, charged particles gyrate around field lines at ω_c.
When E, ∇B, field curvature, or other forces are present, the GUIDING CENTER
drifts across B₀. These drifts are the foundation of particle confinement,
transport, and instability theory (Chen §2, Gurnett & Bhattacharjee §2).

## Derivation Sketch (from Lorentz force → drift formulas)

Starting from `plasma: reasoning.plasma.dispersion_relation_method` (which
provides the general framework for decomposing plasma response):
the single-particle equation is the MICROSCOPIC building block of the
dielectric tensor and dispersion relation.

**General approach** (Chen §2.2): m dv/dt = q(E + v×B). For any slowly-varying
force F (compared to ω_c), the perpendicular drift velocity is:
```
  v_F = (F × B) / (q B²)                                        (general drift)
```
This is obtained by crossing the force equation with B when dv_⟂/dt is
small compared to ω_c v_⟂.

### ∇B DRIFT — gyro-averaging derivation

1. During one gyro-orbit (period T = 2π/ω_c), the particle samples slightly
   stronger B on one side and weaker on the other:
   B(r_GC ± r_L) ≈ B(r_GC) ± r_L · ∇B

2. The Lorentz force qv×B is larger on the strong-field side → smaller
   gyroradius there → orbit is NOT CLOSED; the guiding center drifts
   perpendicular to both B and ∇B.

3. Quantitative: expand Lorentz force to first order in r_L·∇B, average
   over one gyration period (〈v_⟂〉=0, 〈v_⟂(v_⟂·∇)〉=½ v_⟂² ∇_⟂):
   ```
   v_∇B = (½ m v_⟂² / q) (B×∇B) / B³
        = (μ/q) (B×∇B) / B²
   ```
   where μ = m v_⟂² / (2B) is the MAGNETIC MOMENT (first adiabatic invariant).

4. Sign: ions and electrons drift in OPPOSITE perpendicular directions
   because q changes sign. This drives a current J_∇B.

### CURVATURE DRIFT — centrifugal force approach

In a frame following a bent field line, the particle experiences centrifugal
pseudo-force F_cf = m v_∥² R̂_c / R_c, where R_c is the local radius of
curvature and R̂_c is the outward normal perpendicular to B. Plug into
general drift formula:
```
  v_c = (m v_∥² / q) (R_c × B) / (R_c² B²)
```
For vacuum fields (∇×B=0, ∇B purely from curvature):
  v_c = (m v_∥² / q) (B×∇B) / B³
Combined ∇B + curvature (vacuum low-β):
  v_total = (m / qB³)(v_∥² + ½ v_⟂²) B×∇B

### GRAVITY DRIFT (or any uniform body force g)

Analogy of E×B: F = m g (true gravity or pseudo-force in rotating frame):
```
  v_g = (m/q) (g × B) / B²
```
Charge-dependent → ion-electron current. Important in astrophysical plasmas
and magnetospheres (centrifugal effects in rotating systems).

### POLARIZATION DRIFT — time-varying E

When E(t) varies slowly, the particle experiences inertia. Take ∂/∂t of
E×B frame transformation: F = −m dE/dt (inertial transverse force).
```
  v_p = (m / qB²) dE/dt
```
Ions dominate (mass ratio m_i/m_e ≫ 1) → polarization current is primarily
ion current. Essential for low-frequency plasma dielectric response.

### GC-validity conditions (all drifts require these)

- **Spatial**: |r_L·∇B| ≪ B → L_B = B/|∇B| ≫ r_L (B varies slowly over gyroradius)
- **Curvature**: |R_c| ≫ r_L (field curvature radius >> gyroradius)
- **Temporal**: ω_c ≫ ω_drift (gyration much faster than drift — slow envelope)
- When these fail: full orbit integration needed (e.g., near magnetic nulls,
  sharp gradients).

## Algorithm (Chen §2)

```
1. Equation: m dv/dt = q(E + v×B). Decompose v = v_∥ + v_⟂.

2. Uniform B (no E): circular motion at ω_c=qB/m, r_L=v_⟂/ω_c.
   Magnetic moment: μ = mv_⟂²/(2B) = const (first adiabatic invariant).

3. E×B DRIFT (uniform E⟂B):
   Transform to E×B frame: E'=0 → v_E = E×B/B².
   ALL particles drift at same velocity (charge-independent!).
   This is the fundamental MHD fluid velocity.

4. ∇B DRIFT (|∇B| ≪ B/r_L, slow spatial variation):
   v_∇B = ±½v_⟂ r_L (B×∇B)/B² = (μ/q)(B×∇B)/B².
   ± sign: ions and electrons drift in OPPOSITE directions → current!

5. CURVATURE DRIFT (field line curvature R_c, |R_c|≫r_L):
   v_c = (mv_∥²/qB²)(R_c×B)/R_c².
   Equivalent to centrifugal force F_cf = mv_∥² R̂_c/R_c in v_F = F×B/qB².

6. COMBINED ∇B + CURVATURE (vacuum field, ∇×B=0 in low-β):
   v_∇B+v_c = (m/qB³)(v_∥²+½v_⟂²) B×∇B.
   Causes CHARGE SEPARATION → electric fields → further drifts.

7. POLARIZATION DRIFT (time-varying E, slow ∂_t):
   v_p = (m/qB²) dE/dt. Ions dominate (mass ratio m_i/m_e ≫ 1).
   Polarization current is essential for low-frequency plasma response.

8. GRAVITY DRIFT (uniform body force g; analog of E×B):
   v_g = (m/q)(g×B)/B². Charge-dependent, ions and electrons separate.
```

## Adiabatic Invariants & Next Step

μ = mv_⟂²/2B (first, from gyration). J = ∮ v_∥ dl (second, from bounce).
Φ = ∫ B·dS (third, flux through drift orbit). All conserved for slow
variations. μ conservation → magnetic mirror: v_∥²=v²−2μB/m → trapped
when B > B₀ (loss cone in velocity space).

**Guiding-center drift-kinetic equation**: the rigorous formalization of
all drifts into a kinetic equation ∂f/∂t + v_g·∇f + v̇·∇_v f = 0 with
v_g = v_∥ b̂ + v_drift. This feeds directly into `plasma: reasoning.plasma.transport_coefficients`
(Braginskii closure uses GC drifts as inputs for particle/heat fluxes).

## Cross-References

- Chen §2, Gurnett & Bhattacharjee §2, Fitzpatrick §2, Bellan §2
- landau-graph: reasoning.adiabatic_invariance (μ conservation → magnetic
  mirror; parent edge provides the adiabatic invariant framework)
- plasma: reasoning.plasma.transport_coefficients (drifts → particle and
  heat fluxes in Braginskii closure; bidirectional: transport relies on
  drift kinematics established here)
- plasma: reasoning.plasma.dielectric_tensor_magnetized (ω_c sign convention
  is handled there; drift formulas here use unsigned ω_c magnitude)
