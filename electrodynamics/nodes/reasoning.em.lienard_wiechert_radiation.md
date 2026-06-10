---
skill_id: reasoning.em.lienard_wiechert_radiation
type: reasoning
summary_50t: >
  Given r₀(t): φ=e/[R−v·R/c]_ret, A=ev/[c(R−v·R/c)]_ret. E,B from
  derivatives with retarded time → 1/R² velocity field + 1/R acceleration
  field. Larmor: P=μ₀q²a²/(6πc). Relativistic: P=(μ₀q²γ⁶/6πc)(a²−(v×a)²/c²).
trigger:
  - computing radiation from accelerating point charge
  - need angular power distribution for arbitrary trajectory
reasoning_role: lw_radiation
parent: reasoning.retarded_green_function
retrieval_cost: 1
---

# reasoning.em.lienard_wiechert_radiation — r₀(t) → E(r,t), dP/dΩ

## Core Picture

The Liénard-Wiechert potentials give the exact EM fields of a point charge
on an arbitrary trajectory r₀(t), evaluated at the RETARDED time t' satisfying
t' = t − |r−r₀(t')|/c (Jackson §14, Griffiths §11).

**Retarded-time constraint detail** (Griffiths 5th Ed. 2023, §11.1.2): the
implicit equation t_ret = t − |r−w(t_ret)|/c encodes the finite speed of light.
The retarded-time gradient is ∂t_ret/∂t = 1/(1−n̂·β) where n̂ = (r−w)/|r−w|,
β = v/c — the relativistic Doppler factor. For β→1 the field compresses into
a forward cone of angular width ~1/γ (relativistic beaming, §11.2). This
connects to `uo.relativistic_intensity` (γ-a₀ scaling) and
`em.synchrotron_radiation` (beaming in circular motion).

## Derivation Sketch (from retarded Green's function → LW)

The retarded potentials from `landau-graph: reasoning.retarded_green_function` are
```
φ(r,t) = (1/4πε₀) ∫ ρ(r',t')/|r−r'| δ(t' − t + |r−r'|/c) dt' d³r'
A(r,t) = (μ₀/4π)  ∫ J(r',t')/|r−r'| δ(t' − t + |r−r'|/c) dt' d³r'
```
For a point charge ρ=eδ(r'−r₀(t')), J=ev δ(r'−r₀(t')). Doing the r' integral
collapses everything onto the trajectory; the remaining t' integral has the
δ-function constraint t' = t − R(t')/c (implicit equation for retarded time t').

**Key step — Jacobian of the δ-function**: using δ(g(t'))=δ(t'−t*)/|g'(t*)|,
```
g(t') = t' − t + R(t')/c,    g'(t') = 1 − (n·v)/c ≡ κ
```
(R is the distance from source at t' to observation point at t; dR/dt' = −n·v.)
So the t' integral picks up a factor 1/κ, giving the LW potentials below.

**Fields by implicit differentiation**: t' depends on (r,t) via t' + R(r,t')/c = t.
Differentiate at fixed r vs at fixed t:
```
∂t'/∂t |_r  = 1/κ           (one more 1/κ when ∂/∂t hits [·]_ret)
∇t' |_t      = −n/(κc)       (one more 1/κ when ∇ hits [·]_ret)
```
Applying E = −∇φ − ∂A/∂t with these rules and ∂κ/∂t' = ... gives the κ³ in
the denominators below: 1/κ from the potential, ×1/κ from differentiating
[·]_ret, ×1/κ from differentiating κ itself → 1/κ³.

The (1−v²/c²) in the velocity field is the special-relativistic correction
that converts the Coulomb-like 1/R² field into the Lorentz-boosted form of
a uniformly moving charge — it must reduce to (1−β²)/(1−β²cos²θ_v)^{3/2} for
uniform motion.

## Algorithm

```
1. LW potentials (SI):
   φ(r,t) = (e/4πε₀) [1/(κR)]_ret
   A(r,t)  = (μ₀e/4π) [v/(κR)]_ret
   where R = r−r₀(t'), κ = 1−n·v/c, n=R/R. [·]_ret = evaluate at t'.

2. Fields from potentials (using chain rule above, ∂t'/∂t=1/κ, ∇t'=−n/(κc)):
   E = (e/4πε₀)[(n−v/c)(1−v²/c²)/(κ³R²)]_ret           ← VELOCITY field, 1/R²
     + (e/4πε₀c²)[n×((n−v/c)×a)/(κ³R)]_ret            ← ACCELERATION field, 1/R
   B = n×E/c

   Velocity field = boosted Coulomb (no radiation, energy bound to charge).
   Acceleration field = radiation (energy escapes to infinity, ∝1/R).

3. Radiation power: dP/dΩ|_t' = r²⟨S⟩·κ
                              = (e²/16π²ε₀c³)|n×((n−v/c)×a)|²/κ⁵.
   (Extra κ in conversion dt → dt' since dt = κ dt' for emitter clock.)
```

## Special Cases

**Larmor formula** (v≪c): P = μ₀e²a²/(6πc) = e²a²/(6πε₀c³).
Non-relativistic, isotropic pattern ∝ sin²θ (θ from acceleration direction).

**Relativistic Larmor** (Liènard): P = (μ₀e²γ⁶/6πc)[a² − |v×a|²/c²].
γ⁶ factor → radiation increases dramatically at high energy.

**Instantaneous circular motion** (synchrotron): a⟂v → P ∝ γ⁴.
**Linear acceleration** (bremsstrahlung): a∥v → P ∝ γ⁶ (much stronger!).

**Angular distribution** (relativistic): beamed forward into cone Δθ∼1/γ.

## Cross-References

- Jackson §14, Griffiths §11, Lechner §7-8, Landau Vol.2 §63-66
- landau-graph: knowledge.em.lienard_wiechert (LW potential formulas)
- landau-graph: knowledge.em.synchrotron_radiation (special case: uniform B)
