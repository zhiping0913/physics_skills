# Vol.2 Rewrite Fixes — ALL APPLIED 2026-05-26

Date: 2026-05-26.

---

## Fix 1: lorentz_invariance_to_action — Sign determination via min action

**Node**: `reasoning.lorentz_invariance_to_action`
**Priority**: med
**What to fix**: Emphasize that the negative sign in S = −mc∫ds is forced
by requiring the action to have a MINIMUM for small worldline segments.
∫ds is MAXIMIZED along the straight worldline, so only −∫ds is minimized.
This is the same logic as Vol.1 §2 (minimum vs extremum issue), applied
here to determine the sign of the action.
**Where**: Core Picture or Key Insight section.

---

## Fix 2: action_decomposition_field_theory — Missing derivation steps

**Node**: `reasoning.action_decomposition_field_theory`
**Priority**: med
**What to fix**: Add two missing steps to Algorithm:
- Step 5: Sign of a: (∂A/∂t)² must enter with + in S_f, otherwise
  the action can be made arbitrarily negative (no minimum). → a = −1/16π.
- Step 6: Pseudoscalar term ε^{iklm}F_{ik}F_{lm} is a total 4-divergence,
  so it doesn't affect field equations. Excluded automatically.
**Where**: Algorithm section, after current step 4.

---

## Fix 3: gauge_invariance_to_field_tensor — Charge conservation connection

**Node**: `reasoning.gauge_invariance_to_field_tensor`
**Priority**: low
**What to fix**: Add note that gauge invariance and charge conservation
are deeply connected (Landau §18 footnote). ∂_μ j^μ = 0 follows from
gauge invariance of the action.
**Where**: Cross-References or Connections section.
