# Volume 4 Rumination Report — REDO

Date: 2026-05-26. Re-read §5 (EM quantization), §20 (Dirac equation) with nodes loaded.

---

## 1. second_quantization — Three Gaps

### Missing: Photon picture as the ONLY adequate description
Landau §5 opens with: "Описание поля как совокупности фотонов есть
единственное описание, вполне адекватное физическому смыслу
электромагнитного поля в квантовой теории."

This is a strong foundational claim: the photon picture REPLACES the
classical field description — it's not just an alternative. Our template
presents it as "a bridge" rather than the UNIQUE quantum description.

### Missing: Classical limit depends on measurement timescale
Landau: "если велики все числа N_ka, то при суммировании по всем
состояниям энергия поля во всяком случае окажется бесконечной...
Физически осмысленная постановка вопроса об условиях квазиклассичности
основана на рассмотрении значений поля, усредненных по некоторому
небольшому промежутку времени Δt."

The classical limit is NOT simply "N_k ≫ 1." Only modes with ωΔt ≤ 1
contribute to the time-averaged field. The number of such modes is finite
(∝ 1/(cΔt)³), so N_k can be large for each without infinite total energy.
Our template's "large occupation numbers → classical field" is too simplistic.

### Missing: Vacuum fluctuations are ineliminable
Landau: "избежать этого нельзя даже с помощью какой-либо формальной
операции вычеркивания (как это можно сделать для энергии поля), так
как в данном случае мы должны были бы сделать это путем некоторого
разумного видоизменения самих операторов Ê, Ĥ (а не их квадратов),
что оказывается невозможным."

Energy zero-point can be subtracted (normal ordering). But ⟨Ê²⟩ = ∞
cannot — you'd need to modify Ê itself, which is impossible. Our template
says "⟨0|Ê²|0⟩ = ∞" but doesn't explain the asymmetry with energy renormalization.

### Priority: high
### Fixes:
1. State that photon picture is the unique quantum description
2. Clarify classical limit condition involving measurement timescale
3. Explain the ineliminability of vacuum field fluctuations

---

## 2. dirac_equation_antiparticles — Two Gaps

### Missing: Why mass requires TWO coupled spinors
Landau §20: "необходимость введения массы в волновое уравнение требует
одновременного рассмотрения двух спиноров — с помощью лишь одного из
них нельзя составить релятивистски инвариантное уравнение, которое
содержало бы какой-либо размерный параметр."

This is a deep structural fact: a single Weyl spinor can only give a
massless equation (Weyl equation). To introduce mass (a dimensionful
parameter), you MUST couple two spinors. Our template says "4-component
bispinor" but doesn't explain WHY four components are necessary — mass
is the reason.

### Missing: Parity invariance emerges automatically
Landau: "волновое уравнение автоматически оказывается инвариантным
относительно пространственной инверсии." The Dirac equation doesn't
need to ASSUME parity invariance — it FOLLOWS from the two-spinor
structure. Our template mentions charge conjugation but not this.

### Priority: med
### Fixes:
4. Explain why two spinors are required for mass
5. Note that parity invariance is automatic, not assumed

---

## 3. knowledge.qed.dirac_equation — Already Comprehensive
The knowledge node captures the standard representation, plane wave solutions,
non-relativistic limit, and g=2 emergence. No issues.

## 4. knowledge.qed.feynman_rules — Already Comprehensive
Propagators, vertices, Ward identity all correctly stated. No issues.

---

## 5. Hidden Parent Connection
The Dirac equation derivation (§20) uses the same "only available operator"
constraint logic as Vol.1 §4 (only r, t, v available → L=L(v²)) and Vol.2
§8 (only ds available → S=−mc∫ds). This reinforces symmetry_drives_physics
as the correct parent. Already connected.

---

## 6. Summary

| # | Node | Issue | Priority |
|---|------|-------|---------|
| 1 | second_quantization | Photon picture as unique description | high |
| 2 | second_quantization | Classical limit needs measurement timescale | high |
| 3 | second_quantization | Ineliminable vacuum field fluctuations | med |
| 4 | dirac_equation | Two spinors required for mass | med |
| 5 | dirac_equation | Parity invariance is automatic | med |

Rewrite fixes: 5 (2 high, 3 med). No new hidden parents.
