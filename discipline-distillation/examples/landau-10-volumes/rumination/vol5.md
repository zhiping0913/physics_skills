# Volume 5 Rumination Report

Date: 2026-05-26. Re-read key sections. One important finding.

---

## 1. thermodynamic_perturbation_theory — Hidden Cancellation

### Issue
Landau §32 footnote notes a crucial subtlety: "при разложении... мы, строго
говоря, разлагали по величине V/T, пропорциональной числу частиц и потому
отнюдь не малой. Однако логарифмирование и повторное разложение приводят
ко взаимному сокращению больших членов, в результате чего получается ряд
по степеням малой величины."

The expansion of exp(−V/T) has V/T ∝ N ≫ 1 — NOT small for macroscopic
bodies! But taking log Z and re-expanding causes the large terms to cancel,
leaving a series in the genuinely small per-particle perturbation.

Our template's Algorithm says "expand exp(−(H₀+V)/T)" without noting this
subtlety. An agent following the algorithm literally would expand in a
non-small parameter and think the method fails.

### Fix: Add to Key Insight section
Note that V/T is extensive (∝ N), so the naive expansion appears invalid.
The free energy F = −T ln Z, however, involves a LOGARITHM. The large
terms cancel upon taking ln, leaving a series in the per-particle
perturbation |V|/(NT) ≪ 1.

### Priority: high

### Where: After current Key Insight section, or as a note in Algorithm step 2.

---

## 2. ensemble_logic — No Issues Found

Template correctly captures the fundamental move from deterministic
mechanics to probabilistic description. The Gibb's method is correctly
presented as a derived (not assumed) distribution.

---

## 3. microcanonical_to_canonical — No Issues Found

Template correctly captures the derivation: microcanonical for total
system → integrate over environment → expand S'(E^(0)−E_n) → w_n ∝ exp(−E_n/T).

---

## 4. partition_to_thermodynamics — No Issues Found

F = −T ln Z, all thermodynamics from derivatives. Clear and correct.

---

## 5. Hidden Parent Nodes — None New

Vol.5's reasoning nodes already sit at the right level in the tree.
The perturbation theory pattern (F = F₀ + ⟨V⟩ − (1/2T)⟨ΔV²⟩) mirrors
Vol.1 §28 and Vol.3 §38, but these are already connected via analogy edges.

---

## 6. Summary

### Rewrite fixes: 1 (high priority)

| # | Node | Issue | Priority |
|---|------|-------|---------|
| 1 | thermodynamic_perturbation_theory | Missing cancellation of large extensive terms in ln Z | high |

### No new hidden parent nodes.
### No reference-level fixes needed.
