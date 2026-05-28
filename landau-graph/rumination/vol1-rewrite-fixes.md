# Rewrite Fixes from Vol.1 Rumination — ALL APPLIED 2026-05-26

Date: 2026-05-26. These require changes to the node body content
(not just parent references or graph edges).

---

## Fix 1: symmetry_to_conservation — Add 2s-1 counting theorem

**Node**: `reasoning.symmetry_to_conservation`
**What to add to Core Picture**:
Landau §6 opening statement: closed system with s degrees of freedom
has exactly 2s-1 independent integrals of motion. Among these, only 7
(E, P_x, P_y, P_z, M_x, M_y, M_z) are ADDITIVE. Additivity is what
makes them universally useful across all mechanical systems — the
remaining 2s-8 integrals are system-specific and not universal.

**Where**: After current Core Picture paragraph, before Algorithm.

---

## Fix 2: symmetry_to_conservation — Distinguish energy derivation

**Node**: `reasoning.symmetry_to_conservation`
**What to fix in Algorithm**:
Current template lumps energy, momentum, angular momentum into same
"Case A/Case B". But Landau's derivation for energy uses the E-L
equations directly (dL/dt manipulation), while momentum and angular
momentum use infinitesimal symmetry transformations. These are
structurally different derivations and should be separated:
- Energy: uses ∂L/∂t=0 → manipulate dL/dt → conserved quantity
- Momentum/Angular momentum: uses δL=0 under transformation → conserved quantity

**Where**: Algorithm section — split into "Energy (time translation)"
and "Momentum/Angular Momentum (space translations/rotations)".

---

## Fix 3: symmetry_to_conservation — Additivity as central criterion

**Node**: `reasoning.symmetry_to_conservation`
**What to add to Core Picture**:
Landau emphasizes: there are 2s-1 integrals, but only the ADDITIVE
ones (E, P, M) are "especially important." Why? Because additivity means
for non-interacting parts, Q = Σ Q_a. This makes them useful for
collision problems: knowing E,P,M before interaction determines them
after interaction, regardless of what happens during.

---

## Fix 4: variational_principle — Minimum vs Extremum

**Node**: `reasoning.variational_principle`
**What to add to Edge Cases**:
Landau §2 footnote: "принцип наименьшего действия не всегда справедлив
для всей траектории в целом, а лишь для каждого из достаточно малых
ее участков." The action is only guaranteed to be minimal for small
segments of the trajectory. For the full trajectory, it may be
EXTREMAL but not minimal. This becomes crucial in relativistic mechanics
(Vol.2 §8) where S = −mc∫ds: since ∫ds is maximized along a straight
worldline, the negative sign makes S MINIMIZED. The sign choice is
determined by the requirement that S have a minimum for small segments.

**Where**: Edge Cases section — add as first item.

---

## Fix 5: variational_principle — Why L depends only on q,q̇

**Node**: `reasoning.variational_principle`
**What to add to Assumptions**:
Landau: "тот факт, что функция Лагранжа содержит только q и q̇..."
because the mechanical state is FULLY determined by coordinates and
velocities. This is a fundamental assumption of classical mechanics —
if the state at one time is not fully determined by (q,q̇), we would
need higher derivatives in L. This fails for:
- Radiation reaction (Abraham-Lorentz force depends on acceleration)
- Some effective field theories with higher-derivative terms
- Non-local theories

---

## Fix 6: homogeneity_to_scaling — k=-2 edge case

**Node**: `reasoning.homogeneity_to_scaling`
**What to add to Edge Cases**:
When k = -2 (U ∝ 1/r²): β ∝ α², unlike all other k. The scaling
behavior of time vs length is qualitatively different. Example:
potential between two parallel line charges.

---

## Fix 7: homogeneity_to_scaling — Connection to Π-theorem

**Node**: `reasoning.homogeneity_to_scaling`
**What to add to Core Picture or Notes**:
The mechanical similarity argument is the Π-theorem (Buckingham) in
mechanical form. 3 parameters (mass, length, energy) with dimensions
[M,L,T] → exactly 1 dimensionless combination. A note connecting this
to dimensional analysis as a general reasoning pattern.

---

## Fix 8: adiabatic_invariance — Require integrability

**Node**: `reasoning.adiabatic_invariance`
**What to add to Edge Cases**:
The derivation requires the unperturbed motion to be expressible as
p = p(q;E,λ) — possible only for INTEGRABLE systems (1D bounded motion,
or separable multi-DOF systems). For non-integrable systems (e.g.,
3-body problem, chaotic systems), the concept of adiabatic invariant is
not well-defined. Template FAILS for non-integrable systems.

---

## Fix 9: adiabatic_invariance — Fictitious orbit averaging

**Node**: `reasoning.adiabatic_invariance`
**What to clarify in Algorithm step 3**:
Landau explicitly: "усреднение производится по такому движению системы,
какое имело бы место при заданном постоянном значении λ." The average
is over the FICTITIOUS orbit with λ held constant, NOT the true orbit.
This is a fundamental subtlety — the true orbit doesn't even close,
but we average over the closed orbit of the λ=constant system.

---

## Fix 10: adiabatic_invariance — Quantum bridge prominence

**Node**: `reasoning.adiabatic_invariance`
**What to move to Key Insight**:
I = ∮p dq / 2π is exactly the quantity that becomes quantized:
I = nℏ (Bohr-Sommerfeld). The adiabatic invariant is THE bridge from
classical mechanics to old quantum theory. This connection is historically
how quantization was first discovered. Currently in "Connections" —
should be in "Key Insight" section.

---

## Summary

| # | Node | Type | Priority |
|---|------|------|---------|
| 1 | symmetry_to_conservation | Add 2s-1 counting | high |
| 2 | symmetry_to_conservation | Split E vs P/M derivation | high |
| 3 | symmetry_to_conservation | Additivity as central | high |
| 4 | variational_principle | Min vs extremum | med |
| 5 | variational_principle | Why L depends on q,q̇ | med |
| 6 | homogeneity_to_scaling | k=-2 edge case | low |
| 7 | homogeneity_to_scaling | Π-theorem connection | low |
| 8 | adiabatic_invariance | Require integrability | high |
| 9 | adiabatic_invariance | Fictitious orbit averaging | med |
| 10 | adiabatic_invariance | Quantum bridge prominence | med |
