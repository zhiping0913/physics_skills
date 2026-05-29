# Volume 3 Rumination Report — REDO

Date: 2026-05-26. Re-read §1-3, §17, §38 with graph nodes loaded, compared line by line.

---

## 1. quantum_superposition — Missing Foundational Depth

### Missing: QM contains AND needs classical mechanics
Landau §1 makes a uniquely profound point that appears NOWHERE in our templates:
"Формулировка же основных положений квантовой механики принципиально
невозможна без привлечения механики классической."

Quantum mechanics is unique among physical theories: it contains classical
mechanics as its limiting case AND simultaneously needs classical mechanics
for its own logical foundation (measurement requires a classical apparatus).
This is not a side note — it's the philosophical core of QM's relationship
to classical physics.

Our template briefly mentions measurement in the superposition node but misses
this deep epistemological structure.

### Missing: Phase ambiguity of the wave function
Landau §2: "нормированная волновая функция определена лишь с точностью до
постоянного фазового множителя вида e^{iα}... Эта неоднозначность
принципиальная и не может быть устранена."

The phase ambiguity of Ψ is a PRINCIPLED non-uniqueness — not an accidental
one. This is the seed of gauge theory (U(1) symmetry of QM wave functions).
Our template doesn't mention it at all.

### Missing: The normalization and continuous spectrum
Landau §2: "интеграл от |Ψ|² может расходится и тогда Ψ не может быть
нормирована условием (2.2)." Normalization fails for continuous spectrum
states (plane waves). This is mentioned as an Edge Case nowhere in our template.

### Priority: high
### Fixes needed:
1. Add "QM needs classical mechanics" to Core Picture of superposition node
2. Add phase ambiguity as an Assumption or Edge Case
3. Add continuous spectrum normalization to Edge Cases

---

## 2. classical_to_quantum_correspondence — Missing Caveat

### Issue: The potential energy is EMPIRICAL, not derived
Landau §17 footnote: "Это утверждение не является, конечно, логическим
следствием основных принципов квантовой механики и должно рассматриваться
как следствие опытных данных."

When writing Ĥ = −(ℏ²/2m)Δ + U(r), the kinetic term −(ℏ²/2m)Δ IS derived
from p²/2m via the operator substitution. But the potential term U(r) is
simply COPIED from classical mechanics — it is NOT a necessary consequence
of quantization. Our template presents Ĥ = H(p→−iℏ∇, q) as if it's a
unified prescription, without noting that the potential energy part is
empirically motivated, not logically derived.

### Priority: med
### Fix: Add to Algorithm step 2 or As Assumptions: "The potential energy
U(r₁,r₂,...) is taken from classical mechanics by empirical correspondence,
not derived from quantization."

---

## 3. quantum_perturbation_theory — Three Missing Details

### Missing 1: Normalization condition at first order
Landau §38: c_n^(1) must be chosen as 0 to keep ψ_n normalized to first order.
"оно должно быть выбрано так, чтобы функция ψ_n была нормирована с точностью
до членов первого порядка включительно. Для этого надо положить c_n^(1)=0."

Our template's Algorithm steps don't mention this. The wave function correction
ψ_n^(1) is orthogonal to ψ_n^(0) — this is a deliberate choice, not automatic.

### Missing 2: Why E_0^(2) is always negative
Template says "ALWAYS negative for ground state" without explanation. For n=0
(ground state), all E_m > E_0, so E_0 − E_m < 0 for all m, thus E_0^(2) < 0.
The explanation is simple but necessary for understanding.

### Missing 3: The secular equation in the degenerate case
Template says "solve det|V_{αβ}−E^(1)δ_{αβ}|=0" but doesn't explain that the
secular equation gives the FIRST-ORDER energy corrections within the degenerate
subspace — these are the eigenvalues of V restricted to that subspace.

### Priority: med
### Fixes:
1. Add normalization step to Algorithm
2. Add brief explanation of ground-state negativity
3. Expand degenerate case explanation

---

## 4. wkb_quasiclassical — Already Fixed in Vol.1 Rumination

No new issues. The critical fixes (integrability requirement, fictitious
orbit, quantum bridge) were applied during Vol.1 rumination.

---

## 5. Summary of Fixes

| # | Node | Issue | Priority |
|---|------|-------|---------|
| 1 | quantum_superposition | QM needs classical mechanics for its foundation | high |
| 2 | quantum_superposition | Phase ambiguity of Ψ (gauge seed) | high |
| 3 | quantum_superposition | Continuous spectrum normalization failure | med |
| 4 | classical_to_quantum | Potential U is empirical, not derived | med |
| 5 | quantum_perturbation | Normalization c_n^(1)=0 | med |
| 6 | quantum_perturbation | Why E_0^(2) always negative | med |
| 7 | quantum_perturbation | Secular equation explanation | low |

### Rewrite fixes: 7 (2 high, 4 med, 1 low).
### No new hidden parent nodes.
