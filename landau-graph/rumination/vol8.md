# Volume 8 Rumination Report

Date: 2026-05-27. **Redo** — first pass (2026-05-26) found "No Issues, templates clean."
This was diagnostically wrong. Full re-read of §77, §82, §80, §103, §76 + all 6 nodes
found **20 issues** across all nodes.

Methodology: Full re-read with all 6 nodes loaded, paragraph-by-paragraph comparison
using the rumination check-patterns checklist.

---

## 1. reasoning.causality_to_analyticity — 4 issues found

### 1.1 Missing E(t) separation rationale
§82 line 11341 footnote: E(t) is explicitly separated in (77.3) to avoid a
δ-function singularity in f(τ) at τ=0. Without this, the integral formulation
is ill-defined. The node presented (77.3) without this physical justification.
**Check pattern #1** (hidden foundational premise in footnotes).

### 1.2 Missing UHP no-zeros theorem
§82 proves: ε(ω) takes NO real values in any finite UHP point except the
imaginary axis. On the imaginary axis: ε(ω) real, monotonically decreasing
from ε₀>1 (or +∞ for metals) at ω=i0 to 1 at ω=i∞. Implies: ε(ω) has no
zeros in UHP. The node only said "no singularities" — but the theorem about
zeros is equally important (guarantees no resonant enhancement without absorption).

### 1.3 KK asymmetry not mentioned
§82 explicitly notes (82.8)→ε' is "safe" (any ε''>0 works), (82.7)→ε'' is not
(doesn't guarantee ε''>0). This is practically crucial for data analysis. The
node presented both formulas symmetrically.
**Check pattern #10** (template omits non-obvious practical constraint).

### 1.4 ε(−ω*)=ε*(ω) for complex ω
The symmetry generalizes from real ω (77.7) to complex ω (82.2). The node only
gave the real-ω version. The complex version implies ε(iω'') is real on the
imaginary axis — this is used in the monotonicity proof.

---

## 2. reasoning.spatial_dispersion — 5 issues found (+ 1 ghost child)

### 2.1 Ghost child: knowledge.continuous.longitudinal_transverse
Node `reasoning.spatial_dispersion` listed a child that doesn't exist.
Fixed: removed from children list.

### 2.2 ε_l(k≠0) does NOT diverge at ω→0
§103 line 14604: The ω=0 pole in ε(ω) for conductors is an artifact of k=0.
For k≠0, ε_l(k,ω) remains finite — no subtraction needed in KK. This is one
of the most important qualitative consequences of spatial dispersion. The node
mentioned it briefly but didn't emphasize it as a Key Insight.
**Check pattern #7** (qualitative consequence of parameter change understated).

### 2.3 Why no B-term in the nonlocal response
§103 lines 14528-14530: Could a B-dependent term be added to (103.1)? No need —
E and B are linked by Maxwell (rot E = iωB/c), so B-dependence = dependence on
spatial derivatives of E = already captured by ε_ik(k). The node didn't explain
this non-trivial step.

### 2.4 M=0 convention not explained
§103 lines 14542-14546: With spatial dispersion, the (P,M) split is ambiguous.
Convenient convention: M=0, B=H, absorb all averaged microscopic currents into D.
The node used the ε_l,ε_t formalism without explaining this convention.

### 2.5 Poynting vector modification missing
§103 (103.15): S̄ gets an extra term −(ω/16π)(∂ε_ik/∂k)E_i*E_k. This is a
qualitatively new effect — the energy flux direction is modified by the
k-dependence of the dielectric tensor. The node didn't mention this.
**Check pattern #10** (template omits qualitative new effect).

---

## 3. knowledge.continuous.kramers_kronig — 3 issues

### 3.1 Conductor KK formula incomplete
§82 (82.9): ε''(ω) = −(1/π)P∫ε'(x)/(x−ω)dx + 4πσ/ω. The node mentioned
the subtraction form but not the full form with explicit extra term.

### 3.2 Oscillator strength formulation missing
§82 (82.10-82.11): The standard dispersion formula f(ω) = (m/2π²e²)ωε''(ω),
and the f-sum rule ∫f dω = N, were missing. These are standard reference formulas.

### 3.3 Safe/unsafe KK asymmetry
Same as Fix 1.3 above — important practical guidance missing.

---

## 4. knowledge.continuous.dielectric_dispersion — 3 issues

### 4.1 No thermodynamic energy in absorbing media
§80: "в общем случае произвольной дисперсии оказывается невозможным какое-либо
разумное определение электромагнитной энергии как термодинамической величины."
The node gave the energy formula without this fundamental caveat.

### 4.2 "ε'' = 0" → "ε'' ≈ 0"
§80 insists ε'' never truly vanishes at any ω≠0 (has principle significance).
"Transparency" means ε'' ≪ ε', not ε'' = 0.

### 4.3 ε' can be negative
§80: ε'' > 0 is enforced by second law, but ε' has NO sign constraint. The
node didn't mention this (relevant for metamaterials, plasmonics).

---

## 5. knowledge.continuous.moving_media_electrodynamics — 4 issues

### 5.1 Exact Minkowski forms missing
§76 derives EXACT forms (76.9) valid at any v/c, then linearizes. The node
only showed the linearized forms.

### 5.2 4-tensor foundation omitted
§76 uses F_μν and H_μν 4-tensors — D and H form a tensor, not vectors. This
is the relativistic basis of the Minkowski equations. The node skipped it entirely.

### 5.3 Boundary conditions missing
§76 (76.13-76.14) gives explicit boundary conditions for moving interfaces,
which are essential for ROM applications. The node only said "Lorentz-transform back."

### 5.4 Unsourced Minkowski vs Abraham controversy
The node mentioned "Minkowski tensor vs Abraham tensor controversy" — §76 does
not discuss this. It's from later literature, not Landau. Removed.

### 5.5 Velocity gradient caveat
§76 footnote: The Minkowski formulation neglects weak effects from velocity
gradients (gyromagnetic effects, §36). Added as caveat.

---

## 6. knowledge.continuous.spatial_dispersion — 1 issue

### 6.1 Poynting vector modification
Same as Fix 2.5 — the ∂ε_ik/∂k term in S̄ is a qualitatively new effect of
spatial dispersion. Added.

---

## Summary of Changes

| Node | Issues | Type |
|------|--------|------|
| reasoning.causality_to_analyticity | 4 | Content (additions) |
| reasoning.spatial_dispersion | 5 + 1 ghost | Content + topology |
| knowledge.continuous.kramers_kronig | 3 | Content (additions) |
| knowledge.continuous.dielectric_dispersion | 3 | Content (corrections) |
| knowledge.continuous.moving_media_electrodynamics | 4 | Content (rewrite section) |
| knowledge.continuous.spatial_dispersion | 1 | Content (addition) |
| **Total** | **20** | |

All fixes applied. Rewrite details in `vol8-rewrite-fixes.md`.

## What Worked Well in Original Extraction

- The parent connection `reasoning.causality_as_constraint → causality_to_analyticity`
  is correct and well-placed.
- The connection from Vol.10 plasma dielectric to Vol.8 spatial dispersion was
  correctly anticipated during Vol.10 rumination.
- The core tensor decomposition ε_ik = ε_t(...) + ε_l(...) was correct.

## Cross-Volume Connections Verified

- Vol.5 §123 ↔ Vol.8 §82: generalized susceptibility → ε(ω) analyticity. Confirmed.
- Vol.10 §29 ↔ Vol.8 §103: plasma ε_l(k,ω) as microscopic instance of spatial dispersion. Confirmed.
- Vol.2 §23 → Vol.8 §76: F_μν tensor foundation for moving media. Added to node.

No new hidden parent nodes discovered for Vol.8 — the existing
`reasoning.causality_as_constraint` parent already captures the key meta-pattern.
