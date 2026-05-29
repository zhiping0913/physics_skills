# Rumination Check Patterns

Recurring issue types discovered across volumes. Use as a checklist during STEP 1 re-reading.

## Checklist: For Every Original Section Read

- [ ] Read Landau's FOOTNOTES — they often contain the most important subtleties
- [ ] Check the OPENING paragraph of each section — Landau states foundational premises there
- [ ] Verify that ALL forms of an equation in the original appear in the template (e.g., adiabatic condition has 4 forms, not 1; Minkowski has exact + linearized forms; FLT has "sea" + "hole" pictures)
- [ ] Check whether the template mentions connections to OTHER chapters within the same volume (e.g., §7→§15 in Vol.6)
- [ ] Look for Landau's explicit "this is not derived" disclaimers (e.g., §17 potential energy is empirical; §1 ε=δE/δn is a definition, not an independent quantity)
- [ ] If the template presents 3-vector equations, check whether Landau uses 4-tensor formalism (F_μν, H_μν) as foundation
- [ ] For every factual claim made by the template, verify it exists in the CITED section — flag anything imported from external knowledge
- [ ] Check whether the template conflates two DISTINCT quantities with similar names (e.g., N(p) vs n(p); ε''≈0 vs ε''=0)
- [ ] For operators with opposite T-parity: their equal-time correlation MUST vanish — does the template note this?

## Recurring Pattern Types

### 1. Hidden foundational premise (opening paragraph + footnote trap)
Vol.6 §1: "physically infinitesimal volume" — continuum premise
Vol.6 §1: Eulerian description framing (v(x,t) at fixed point)
Vol.3 §1: QM needs classical mechanics for its own foundation
Vol.8 §82 fn: E(t) term separated in (77.3) specifically to avoid δ-function
  singularity in f(τ) at τ=0 — without this separation the integral is ill-defined.
  Footnote justifies a formula choice that otherwise seems arbitrary.

### 2. Hidden connection within the same volume
Vol.6 §7→§15: momentum flux Π_ik is foundation for Navier-Stokes
Vol.5 §32: ln Z cancellation (extensive V/T → log removes large terms)

### 3. Order of limits / limits do not commute
Vol.10 §29: linearization limit MUST precede ν→0 limit
Vol.1 §2: action is minimal only for small segments, extremal for whole trajectory
Vol.9 §77: Im ε→0 in infinite medium — infinite size FIRST, then Im ε→0.
  Arbitrarily small Im ε ultimately leads to absorption. Transparent-medium
  result depends on this specific ordering.

### 4. Sign determination from minimum principle
Vol.2 §8: negative sign in S=−mc∫ds forced by min-action
Vol.2 §27: a = −1/16π fixed by requiring (∂A/∂t)² with + sign

### 5. Empirical vs derived / definition vs consequence
Vol.3 §17: potential U in Ĥ is empirical, not from quantization
Vol.9 §1: ε = δE/δn — quasiparticle energy is a variational DERIVATIVE, not an
  independent quantity. The self-consistency is deeper than Hartree: interaction
  changes the form of the KINETIC energy operator, not just potential. This is
  WHY m* ≠ m — it's derived, not a free parameter.
Vol.9 §2: m*/m = 1 + ⟨F(ϑ)cosϑ⟩ — derived from Galilean invariance (total
  momentum = mass flux), not an empirical input.

### 6. Multiple equivalent formulations not collapsed
Vol.6 §2: adiabatic condition has 4 distinct forms (ds/dt=0, ∂s/∂t+v·∇s=0, ∂(ρs)/∂t+div(ρsv)=0, s=const)
Vol.1 §6-9: energy derivation differs structurally from momentum/angular momentum derivation
Vol.9 §1: FLT has two equivalent formulations — (a) filled Fermi sea + quasiparticles
  with ε can be negative, (b) "hole" picture with ε≥0, μ=0, excitations in pairs.
  Templates that present only one formulation miss the alternative that eliminates
  the "unobservable filled Fermi sphere."

### 7. Counting / classification the template misses
Vol.1 §6: 2s−1 integrals, only 7 additive
Vol.3 §2: phase ambiguity (stem of U(1) gauge), continuous spectrum normalization failure

### 8. Gauge → conservation connections
Vol.2 §18 footnote: gauge invariance and charge conservation are connected

### 9. Symmetry emerges from structure, not imposed
Vol.4 §20: Dirac equation — parity invariance is automatic from γ-matrix algebra,
  not separately imposed. Landau presents it as a consequence, not a requirement.
  Check: does the template say "we impose X symmetry" when Landau says "X follows
  from Y"?
Vol.1 §6-9: energy conservation emerges from time homogeneity, not imposed.

### 10. Template omits a non-obvious decomposition or counting step
Vol.7 §4: why exactly TWO elastic constants for isotropic body? Because only two
  independent quadratic scalar invariants from the strain tensor. Template said
  "two constants" without the counting reasoning.
Vol.3 §38: normalization condition c_n^(1)=0 is a hidden step in perturbation
  theory — template jumps from "expand in λ" to "first-order correction formula"
  without noting the intermediate normalization condition that makes it work.

### 11. Template omits the 4-tensor/relativistic foundation
Vol.8 §76: moving_media node gave flat 3-vector equations, but Landau's entire
  derivation uses F_μν and H_μν 4-tensors. D and H form H_μν — they transform
  as a 4-tensor, not as vectors. This is not decorative formalism; the 4-tensor
  structure reveals the relativistic transformation properties.
  Check: does the template present flat equations where Landau uses 4-tensors?

### 12. Template shows only linearized/approximate form, omitting exact
Vol.8 §76: moving_media node showed only linear-in-v/c forms (76.10-76.11).
  Landau derives EXACT forms (76.9) valid at any v/c, then linearizes as a
  secondary step. The exact result is the general one; the linearized form is
  a special case. Templates that skip the exact form lose generality.
  Check: if the template has a series expansion or approximation, does the
  original also have the EXACT form before expanding?

### 13. Template imports external knowledge not in Landau
Vol.8 §76: moving_media node mentioned "Minkowski vs Abraham tensor controversy"
  — §76 doesn't discuss this at all. It's from later literature, incorrectly
  presented as if from Landau. When a template makes a claim, verify it's
  ACTUALLY in the cited section, not from the writer's general physics knowledge.
  Check: for every factual claim in the node, can you point to the line
  in the original that justifies it? If not, remove or mark as external.

### 14. Template conflates two distinct quantities with similar names/notation
Vol.9 §7: N(p) = true particle distribution (from G(t=−0,r)), n(p) = quasiparticle
  distribution (from FLT §1). These are FUNDAMENTALLY different quantities, but
  the Green's function template used "N" without clarifying it refers to TRUE
  particles, not quasiparticles. The quasiparticle concept emerges from pole
  structure, not equal-time limits.
Vol.8 §80: "ε'' = 0 in transparent regions" — Landau insists ε'' is NEVER truly
  zero at any ω≠0 ("имеет существенное принципиальное значение"). "Small" ≠ "zero."
  Check: does the template use a symbol or term that the original reserves for
  a DIFFERENT quantity? Does the template say a quantity "is zero" when the
  original says it "is very small but never strictly zero"?

### 15. T-parity → equal-time correlation structure
Vol.9 §76: E (T-even) and B (T-odd) have opposite time-reversal parity. Their
  cross-correlation function is therefore ODD in t → vanishes at t=0.
  Consequence: ⟨E_i B_k⟩=0 at equal times → ⟨Poynting vector⟩=0 in equilibrium.
  This is a general principle: operators with opposite T-parity have zero
  equal-time correlation. Templates often miss these symmetry-dictated
  correlation constraints, which are as rigid as conservation laws.
  Check: if the template mentions two operators, check their T-parities.
  If opposite: their equal-time correlation MUST vanish — does the template
  note this?
