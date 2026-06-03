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

## Algorithm

```
1. LW potentials (SI):
   φ(r,t) = (e/4πε₀) [1/(κR)]_ret
   A(r,t)  = (μ₀e/4π) [v/(κR)]_ret
   where R = r−r₀(t'), κ = 1−n·v/c, n=R/R. [·]_ret = evaluate at t'.

2. Fields from potentials (chain rule ∂/∂r → ∂/∂t'):
   E = (e/4πε₀)[(n−v/c)(1−v²/c²)/(κ³R²)]_ret
     + (e/4πε₀c²)[n×((n−v/c)×a)/(κ³R)]_ret
   B = n×E/c

   First term ∝ 1/R²: VELOCITY FIELD (generalized Coulomb, no radiation).
   Second term ∝ 1/R: ACCELERATION FIELD (radiation, energy to infinity).

3. Radiation power Poynting: dP/dΩ = r²⟨S⟩ = (e²/16π²ε₀c³)|n×((n−v/c)×a)|²/κ⁵.
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
