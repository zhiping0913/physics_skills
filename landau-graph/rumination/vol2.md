# Volume 2 Rumination Report

Date: 2026-05-26. Re-read key sections with graph nodes loaded.

---

## 1. lorentz_invariance_to_action — Issues Found

### Missing: Sign determination via minimum action
Landau §8 explicitly uses the minimum action principle to fix the sign:
"интеграл ∫ds имеет максимальное значение вдоль прямой мировой линии;
поэтому интеграл, взятый с положительным знаком, не может иметь минимума;
взятый же с обратным знаком он имеет минимум."

The sign choice S = -mc∫ds (negative) is FORCED by requiring the action
to have a minimum for small worldline segments. Our template mentions
this but doesn't emphasize that this is the SAME logic as Vol.1 §2
(minimum vs extremum issue). The relativistic case is actually where
this distinction becomes crucial — the straight worldline MAXIMIZES ∫ds,
so only the negative sign yields a true minimum.

### Missing: The constant term -mc² in L
When matching to classical limit, Landau drops the constant -mc² from
L because "постоянные члены в функции Лагранжа не отражаются на
уравнениях движения." Our template's Worked Example shows the expansion
but doesn't explain WHY the constant can be dropped — it's L's
non-uniqueness (add dF/dt). This is a key step that an agent might
not understand without the context.

### Priority: med
**Where**: Add to Core Picture that the sign determination uses min-action logic.

---

## 2. action_decomposition_field_theory — Issues Found

### Missing two steps in derivation chain
Landau's §27 reasoning is remarkably complete. Our template captures steps 1-4
(superposition→linear equations, gauge→F_ik, scalar→F², form of S_f)
but MISSES:

**Step 5 — Sign of S_f**: Landau argues that (∂A/∂t)² must enter with +
because otherwise "достаточно быстрым изменением потенциала со временем
всегда можно было бы сделать S_f отрицательной величиной со сколь угодно
большим абсолютным значением; S_f не могло бы, следовательно, иметь
минимума." This is the same minimum-action logic applied to field theory.
→ Fixes a = -1/(16π) in Gaussian units.

**Step 6 — Pseudoscalar exclusion**: The quantity ε^{iklm}F_{ik}F_{lm} is a
total 4-divergence, so adding it to S_f doesn't change field equations.
Landau notes this is "interesting" because it excludes the pseudoscalar
"независимо от того обстоятельства, что она представляет собой не истинный,
а псевдоскаляр." Our template should mention this — it's a beautiful example
of how mathematical structure (total derivative) reinforces physical
constraints (pseudoscalar can't appear in a scalar action).

### Priority: med
**Where**: Add steps 5 and 6 to Algorithm section.

---

## 3. gauge_invariance_to_field_tensor — Minor Issue

### Missing: Connection to charge conservation
Landau's footnote to §18: "калибровочная инвариантность уравнений
электродинамики и сохранение заряда тесно связаны друг с другом."
Gauge invariance and charge conservation are two aspects of the same
underlying principle. Our template's Cross-References mention "Modern:
gauge principle is the foundation of all fundamental interactions"
but don't note the specific connection: gauge invariance → ∂_μ j^μ = 0.

### Priority: low
**Where**: Add to Cross-References or Connections.

---

## 4. retarded_green_function — No Issues Found

Template correctly captures the causal boundary condition reasoning.
The step-by-step derivation from □φ = -4πρ → φ = χ(t-R/c)/R → 
Coulomb near-field → φ = de_{t-R/c}/R → superposition is complete.

Minor note: the template could mention that the choice f₂=0 (excluding
advanced solution) is equivalent to the physical boundary condition
"radiation goes OUT from source, not IN." Currently implicit — could
be explicit.

---

## 5. multipole_expansion_radiation — No Issues Found

Template correctly captures the scale-separation logic (a/λ ≪ 1 → 
retardation negligible → dipole dominates). The connection to
small_parameter_expansion in Vol.1 is properly noted in Cross-References.
The validity section correctly states both conditions (a≪λ AND R₀≫λ).

---

## 6. Hidden Parent Node: causality_as_constraint

Three reasoning patterns share a common premise:
- **retarded_green_function** (Vol.2): causality → retarded solution
- **causality_to_analyticity** (Vol.8): causality → analytic ε(ω) → Kramers-Kronig
- **fluctuation_dissipation_quantum** (Vol.9): causality → FDT

All use the principle that "response cannot precede cause" as a CONSTRUCTIVE
tool to determine the form of physical laws. This could be extracted as:
`reasoning.causality_as_constraint`.

### Priority: high for cross-volume unification
Children: retarded_green_function, causality_to_analyticity, fluctuation_dissipation_quantum

---

## 7. Cross-Volume Connections Missed

| Vol.2 node | Should connect to | Type |
|-----------|-------------------|------|
| lorentz_invariance_to_action | variational_principle (min action sign logic) | prerequisite |
| retarded_green_function | causality_to_analyticity (Vol.8) | analogy |
| action_decomposition_field_theory | gauge_invariance_to_field_tensor (same §27 uses it) | prerequisite |

---

## 8. Summary of Fixes Needed

### Immediate (reference-level):
- `retarded_green_function` ↔ `causality_to_analyticity`: add analogy edge

### Rewrite (content-level):
| # | Node | Issue | Priority |
|---|------|-------|---------|
| 1 | lorentz_invariance_to_action | Emphasize sign determination via min action | med |
| 2 | action_decomposition_field_theory | Add steps 5 (sign) and 6 (pseudoscalar) | med |
| 3 | gauge_invariance_to_field_tensor | Add gauge→charge conservation connection | low |

### New hidden parent:
- `reasoning.causality_as_constraint` (3 children from Vol.2,8,9)

### Rewrite fixes count: 3 (1 med priority per node)
