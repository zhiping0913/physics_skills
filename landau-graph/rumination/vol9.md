# Volume 9 Rumination Report

Date: 2026-05-27. **Redo** — first pass (2026-05-26) found "No Issues, templates clean."
Full re-read of §1-2, §7, §76-78 + all 5 Vol.9 nodes found **17 issues**.

Methodology: Full paragraph-by-paragraph re-read with all nodes loaded,
using the rumination check-patterns checklist.

---

## 1. reasoning.fermi_liquid_theory — 9 issues found

### 1.1 Missing universal quasiparticle principle
§1 opening (line 170): "Всякое слабо возбужденное состояние макроскопического тела
можно рассматривать в квантовой механике как совокупность отдельных элементарных
возбуждений." This is the foundation for ALL quantum liquid theory, not just FLT.
The node jumped to FLT without this universal framing. Also: only TWO quantum
liquids exist in nature (³He, ⁴He). Helium is special due to weak interaction.
**Check pattern #1** (hidden foundational premise in opening paragraph).

### 1.2 E ≠ Σε — fundamental non-additivity
§1 (line 196): "полная энергия жидкости E отнюдь не сводится к сумме энергий ε
квазичастиц." The node mentioned adiabatic continuity but missed this non-additivity.

### 1.3 ε = δE/δn — self-consistency beyond Hartree
§1 (lines 200-206): ε is the VARIATIONAL derivative, not an independent quantity.
The self-consistency is DEEPER than Hartree: "в гамильтониане атома учитывается
влияние окружающих частиц не только на потенциальную энергию, но меняется также
и зависимость оператора кинетической энергии от оператора импульса." This is WHY
m* ≠ m — the interaction changes the very form of the kinetic energy operator.
**Check pattern #5** (derived nature of key quantity).

### 1.4 Quasiparticle spin always 1/2
§1 (line 210): Regardless of real particle spin, quasiparticle spin in FLT is
always 1/2. For s>1/2, (ŝ·p)² splits degeneracy into (2s+1)/2 branches. The node
said "same quantum numbers as free fermions" without this important subtlety.

### 1.5 ε_F is NEGATIVE at T=P=0
§1 (lines 327-329): At T=0 and P=0, ε_F = μ is negative because −μ = heat of
vaporization per particle (positive). Counterintuitive but correct.

### 1.6 Alternative "hole" picture
§1 (lines 315-325): There is an equivalent formulation with ε≥0 always.
Quasiparticles outside Fermi sphere and "holes" inside, both with μ=0 Fermi
distribution. Excitations appear/disappear in pairs. Eliminates the
"unobservable filled Fermi sphere." The node didn't mention this.

### 1.7 Galilean invariance → m*/m
§2 (2.12): m*/m = 1 + ⟨F(ϑ)cosϑ⟩. This is DERIVED from Galilean invariance
(total momentum = mass flux), not an empirical input. The node mentioned
effective mass without showing where it comes from.
**Check pattern #9** (symmetry emerges from structure, not imposed).

### 1.8 Stability conditions
§2 (lines 456-463): F_l + 1 > 0, G_l + 1 > 0. l=1 → m* > 0. l=0 → positive
compressibility. Essential constraints on the phenomenological f-function.
The node didn't mention these.

### 1.9 ³He quantitative bound
§1 footnote (line 304): For ³He, applicability limited to T ≲ 0.1K while
|ε_F| ≈ 2.5K. This illustrates FLT's limited quantitative scope.

---

## 2. reasoning.green_function_method — 4 issues

### 2.1 Why the method is needed
§7 (lines 948-950): Perturbation theory unwieldy at higher orders. Real
interactions are STRONG — infinite series must be summed → requires QFT
techniques (Galitsky-Migdal, 1958). The node presented the method without motivation.

### 2.2 Ĥ' = Ĥ − μN̂
§7 (line 968): Heisenberg operators use Ĥ', not Ĥ — grand canonical convenience.
At T=0, ground state minimizes ⟨Ĥ'⟩. G depends on μ as parameter. The node
didn't mention this crucial convention.

### 2.3 N(p) ≠ n(p)
§7 (line 1111): G(t=−0) gives the distribution of TRUE particles N(p), NOT
quasiparticles n(p). These are fundamentally different. The quasiparticle
concept emerges from pole structure, not equal-time limit.

### 2.4 t→−0 limit significance
§7 (lines 1125-1133): The −0 sign determines contour closure (upper half-plane).
At T=0: G₀(t=−0,p) = −iθ(p_F−p) → the Fermi step. The node mentioned the
density formula but not the significance of the limit.
**Check pattern #10** (template omits non-obvious step — sign significance).

---

## 3. reasoning.fluctuation_dissipation_quantum — 3 issues

### 3.1 Order of limits: Im ε→0
§77 (lines 11287-11288): Taking Im ε→0 in infinite medium requires ordering:
infinite size FIRST, then Im ε→0. Arbitrarily small Im ε leads to absorption
in infinite medium. The transparent-medium limit depends on this order.
**Check pattern #3** (order of limits / limits do not commute).

### 3.2 Equal-time E-B correlation vanishes
§76 (line 11236): E (T-even) and B (T-odd) → cross-correlation odd in t →
vanishes at t=0. ⟨Poynting vector⟩ = 0 in equilibrium. Elegant consequence.

### 3.3 Nyquist from FDT
§78: x=J(t), f=−ℰ, α(ω)=iω/Z(ω) → (J²)_ω = (ℏω/|Z|²)R(ω)coth(ℏω/2T).
Classical: (ℰ²)_ω = 2T R(ω). Universal — independent of resistance type.
The node mentioned Nyquist without showing the derivation.

---

## 4. knowledge.condensed.green_function — No issues

The knowledge node correctly captures the definitions, spectral representation,
Dyson equation, and Wick theorem from §7-11. No changes needed.

---

## Summary of Changes

| Node | Issues | Type |
|------|--------|------|
| reasoning.fermi_liquid_theory | 9 | Content (major expansion) |
| reasoning.green_function_method | 4 | Content (additions) |
| reasoning.fluctuation_dissipation_quantum | 3 | Content (additions) |
| knowledge.condensed.green_function | 0 | Clean |
| **Total** | **16 + 1 (3He footnote)** | |

All fixes applied. Rewrite details in `vol9-rewrite-fixes.md`.

## What Worked Well

- The Green's function ↔ Fermi liquid prerequisite edge is correct
- The causality_as_constraint parent for FDT is well-placed
- The analogy from adiabatic_invariance to FLT is conceptually valid
- The cross-reference from Vol.10 collision integral to FLT is correct

## Cross-Volume Connections Verified

- Vol.5 §123 (classical FDT) → Vol.9 §76 (quantum FDT): confirmed
- Vol.10 §41 (Landau collision integral) → Vol.9 §1 (quasiparticle kinetics): confirmed
- Vol.4 §103 (QED propagator) → Vol.9 §7 (condensed matter GF): analogy noted

No new hidden parent nodes discovered for Vol.9 — the existing
`reasoning.causality_as_constraint` and `reasoning.classical_to_quantum_correspondence`
parents already capture the patterns.

## Final state after this rumination

All 10 volumes now ruminated. GRAPH.json: 89 nodes, 152 edges.
Pending: final consistency check (optional).
