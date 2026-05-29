# Volume 9 Rewrite Fixes

Status: ALL APPLIED (2026-05-27)

---

## Fix 1: reasoning.fermi_liquid_theory — Universal quasiparticle principle

§1 opening (line 170): "Всякое слабо возбужденное состояние макроскопического тела
можно рассматривать в квантовой механике как совокупность отдельных элементарных
возбуждений." This is the universal foundation for ALL quantum liquid theory, not just
FLT. The node jumps to FLT without this framing. Also: only TWO quantum liquids exist
in nature (³He, ⁴He) — helium remains liquid due to weak interaction.

## Fix 2: reasoning.fermi_liquid_theory — E ≠ Σε

§1 (line 196): "полная энергия жидкости E отнюдь не сводится к сумме энергий ε
квазичастиц." E is a functional of n but NOT ∫nε. The node mentions adiabatic
continuity but misses this fundamental non-additivity. The energy of adding one
quasiparticle depends on the state of ALL others.

## Fix 3: reasoning.fermi_liquid_theory — ε = δE/δn, self-consistency beyond Hartree

§1 (lines 200-206): ε is DEFINED as the variational derivative δE/δn — it is NOT
an independent quantity. Moreover, the self-consistency is DEEPER than Hartree:
"в гамильтониане атома учитывается влияние окружающих частиц не только на
потенциальную энергию, но меняется также и зависимость оператора кинетической
энергии от оператора импульса." The interaction changes the form of the KINETIC
energy operator — this is WHY m* ≠ m, not just a potential shift.

## Fix 4: reasoning.fermi_liquid_theory — Quasiparticle spin always 1/2

§1 (line 210): Regardless of real particle spin, quasiparticle spin in FLT is
always 1/2. For s>1/2, (ŝ·p)² splits levels into (2s+1)/2 doubly-degenerate branches.
The node says "same quantum numbers as free fermions" without this subtlety.

## Fix 5: reasoning.fermi_liquid_theory — ε_F is NEGATIVE at T=P=0

§1 (lines 327-329): At T=0 and P=0, ε_F = μ is negative because −μ equals the
positive heat of vaporization per particle. Quasiparticle energies near ε_F are
therefore negative — counterintuitive but important.

## Fix 6: reasoning.fermi_liquid_theory — Alternative "hole" picture

§1 (lines 315-325): There is an alternative formulation with ε≥0 always.
Quasiparticles outside Fermi sphere (ε=v_F(p−p_F)) and "holes" inside
(ε=v_F(p_F−p)), both with μ=0 Fermi distribution (1.16). Excitations appear/disappear
in pairs. This removes the "unobservable filled Fermi sea."

## Fix 7: reasoning.fermi_liquid_theory — Galilean invariance → m*/m

§2 (2.12): m*/m = 1 + ⟨F(ϑ)cosϑ⟩. This is a DERIVED relation from Galilean
invariance: total momentum = mass flux. The node mentions effective mass without
showing where it comes from.

## Fix 8: reasoning.fermi_liquid_theory — Stability conditions

§2 (lines 456-463): F_l + 1 > 0, G_l + 1 > 0. For l=0: positive compressibility.
For l=1: m* > 0. These constrain the phenomenological f-function. The node doesn't
mention these essential consistency conditions.

## Fix 9: reasoning.fermi_liquid_theory — ³He quantitative bound

§1 footnote (line 304): For liquid ³He, quantitative applicability is limited to
T ≲ 0.1K while |ε_F| ≈ 2.5K. The discrepancy illustrates the theory's limitations.

## Fix 10: reasoning.green_function_method — Why the method is needed

§7 (lines 948-950): Perturbation theory becomes unwieldy at higher orders. Real
interactions are STRONG, so infinite series must be summed. The technique comes
from QFT (Galitsky-Migdal, 1958). The node presents the method without motivation.

## Fix 11: reasoning.green_function_method — Ĥ' = Ĥ − μN̂

§7 (line 968): Heisenberg operators use Ĥ' not Ĥ — grand canonical convenience.
At T=0, ground state minimizes ⟨Ĥ'⟩ not ⟨Ĥ⟩. The Green's function depends on μ
as a parameter. The node doesn't mention this crucial convention.

## Fix 12: reasoning.green_function_method — N(p) ≠ n(p)

§7 (line 1111): N(p) = distribution of TRUE particles (from G(t=−0,r)).
n(p) = quasiparticle distribution (from FLT §1). They are different quantities.
The node's "Thermodynamics: N = −i∫G..." is about true particles, not quasiparticles.

## Fix 13: reasoning.green_function_method — The t→−0 limit

§7 (lines 1125-1133): The −0 limit determines contour closure (upper half-plane
for t<0). N/V = −2i G(t=−0,r=0). This limit gives the FERMI step at T=0.
The node mentions the density formula but not the significance of the limit.

## Fix 14: reasoning.fluctuation_dissipation_quantum — Order of limits: Im ε→0

§77 (lines 11287-11288): Taking Im ε→0 in infinite medium requires the order:
infinite size FIRST, then Im ε→0. Arbitrarily small Im ε ultimately leads to
absorption in infinite medium. The transparent-medium result depends on this
specific ordering. Check pattern #3.

## Fix 15: reasoning.fluctuation_dissipation_quantum — Equal-time E-B correlation

§76 (line 11236): E (T-even) and B (T-odd) → cross-correlation odd in t → vanishes
at t=0. ⟨E_i B_k⟩=0 at equal times → ⟨Poynting vector⟩=0 in equilibrium.

## Fix 16: reasoning.fluctuation_dissipation_quantum — Nyquist from FDT

§78: Elegant derivation of Johnson-Nyquist noise from FDT: identify x(t)=J(t),
f = −ℰ, α(ω)=iω/Z(ω). Then (J²)_ω = (ℏω/|Z|²) R(ω) coth(ℏω/2T). Classical:
(ℰ²)_ω = 2T R(ω). Universal — independent of the nature of the resistance.

## Fix 17: reasoning.green_function_method — G_αβ = δ_αβ G justification

§7 (line 1050): G_αβ is a mixed spinor of rank 2 (α contravariant, β covariant).
The unit mixed spinor is δ_αβ. This is the spinor justification for G_αβ=δ_αβ G
in non-magnetic systems, not just "no preferred direction."
