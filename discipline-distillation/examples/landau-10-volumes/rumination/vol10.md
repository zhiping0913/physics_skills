# Volume 10 Rumination Report

Date: 2026-05-26. Re-read Landau damping and plasma dielectric sections.

---

## 1. landau_damping — Order of Limits

### Issue
Landau §29 footnote emphasizes a crucial subtlety not fully captured by our template:
the derivation involves TWO limits that must be taken in a specific ORDER:

"The reasoning essentially contains two transitions to the limit: to small fields
(linearization of equations) and to ν → 0. Note that the first is performed BEFORE
the second. The necessity of this specific order of limits is connected with the
requirement that δf ≪ f₀ during linearization; at ν = 0, the perturbation δf
would become infinite at kv = ω."

This is subtle: you cannot take the collisionless limit first, because then δf
would diverge at resonance and linearization would fail. You must first linearize
(assuming weak field + some collisions), THEN take ν→0. Our template mentions
two justifications for ω→ω+i0 but doesn't explain WHY the order matters.

### Fix: Add to Algorithm or Key Insight
Explicitly state that the LIMITS DO NOT COMMUTE: the collisionless (ν→0) limit
must be taken AFTER the linearization (small field) limit.

### Priority: high
### Where: Algorithm section, after step discussing Landau's rule.

---

## 2. landau_damping — Thermodynamic Reversibility

### Issue
Landau §30 explicitly states: "бесстолкновительная диссипация не связана с
возрастанием энтропии и потому представляет собой термодинамически обратимый
процесс."

Collisionless dissipation is THERMODYNAMICALLY REVERSIBLE — it does NOT involve
entropy increase. This is the fundamental distinction from ordinary collisional
dissipation. Our template mentions this in passing ("plasma echo experiments
confirm this") but the Key Insight should emphasize this as the DEFINING feature
of Landau damping.

### Fix: Move reversibility statement to Key Insight section.
### Priority: med

---

## 3. plasma_dielectric_response — Spatial Dispersion Link

### Issue
Landau explicitly connects Landau damping to spatial dispersion: "Механизм
затухания Ландау тесно связан с пространственной дисперсией." Our template's
Cross-References mention Vol.8 §103 but the connection should be stronger:
Landau damping IS the dissipative manifestation of spatial dispersion in a
collisionless plasma (k-dependence of ε is essential — without it, Im ε = 0).

### Fix: Add explicit note to Key Insight or Cross-References.
### Priority: low

---

## 4. kinetic_equation_closure — No Issues Found
Template correctly captures Boltzmann and Vlasov as closing the BBGKY hierarchy.

## 5. collision_integral_construction — No Issues Found
Landau collision integral and Boltzmann integral correctly presented.

---

## 6. Summary

### Rewrite fixes: 3

| # | Node | Issue | Priority |
|---|------|-------|---------|
| 1 | landau_damping | Order of limits (linearization before ν→0) | high |
| 2 | landau_damping | Thermodynamic reversibility as defining feature | med |
| 3 | plasma_dielectric_response | Stronger link to spatial dispersion | low |

### No new hidden parent nodes.
