---
skill_id: reasoning.renormalization
type: reasoning
summary_50t: >
  Loop integrals in QFT diverge at high momentum (UV). Regularize with
  cutoff Λ. Bare parameters (m₀,e₀) absorb divergences → physical (m_R,e_R)
  are finite. Renormalizability: only finite # of counterterms needed.
  Running coupling: β(e) = μ de/dμ.
trigger:
  - encountering UV divergence in loop diagrams
  - need to extract finite physical predictions from QFT
  - understanding why QED works despite infinite loop integrals
reasoning_role: uv_completion
parent: reasoning.second_quantization
children:
  - knowledge.qed.feynman_rules
retrieval_cost: 1
---

# reasoning.renormalization — UV Divergence → Finite Predictions

## Core Picture

Quantum field theory produces INFINITY in loop diagrams. Renormalization
is the procedure that extracts FINITE, experimentally verified predictions
from these infinities. It is not a trick or a fudge — it is the statement
that the bare parameters of the Lagrangian are NOT the measured ones.

```
Lagrangian(φ, m₀, e₀) → loop integrals → DIVERGENCES
     ↓
Regularize (cutoff Λ) → finite but Λ-dependent
     ↓
Absorb Λ into m₀(Λ), e₀(Λ) → physical m_R, e_R finite
     ↓
Take Λ → ∞ → all observables expressed in m_R, e_R — FINITE
```

## Where Do Divergences Come From?

A Feynman diagram with L loops involves a momentum integral ∼∫d⁴k.
At large k, propagators behave as 1/k², vertices as constants.
A diagram with E external lines, I internal propagators, V vertices:
```
Superficial degree of divergence: D = 4L − 2I
For QED: D = 4 − E − ³⁄₂F  (F = number of external fermion lines)
```
Only diagrams with E ≤ 4, F ≤ 2 diverge → electron self-energy (E=2,F=2),
vacuum polarization (E=2,F=0), vertex correction (E=3,F=2).

## The Renormalization Procedure

**Step 1: Regularize.**
Introduce a large momentum cutoff Λ, or use dimensional regularization
(d=4−ε). Loop integrals now give finite results that depend on ln Λ.

**Step 2: Relate bare to physical.**
The bare Lagrangian L₀ = ψ̄(i∂̸ − m₀)ψ − ¼F₀² − e₀ψ̄A̸ψ contains
bare parameters m₀, e₀. Physical parameters are measured at a reference
scale μ: m_R = m_R(μ), e_R = e_R(μ).

**Step 3: Counterterms.**
Write m₀ = m_R + δm, e₀ = e_R + δe. The counterterm Lagrangian
L_ct = −δm ψ̄ψ − ¼δZ₃ F² − δe ψ̄A̸ψ adds Feynman rules that
CANCEL the Λ-dependent parts of loop diagrams.

**Step 4: Renormalization conditions.**
Fix δm, δe, δZ_i by requiring that at the scale μ:
- Electron propagator has pole at p² = m_R² with residue 1
- Photon propagator has pole at k² = 0 with residue 1
- Vertex function at zero momentum transfer equals e_R

**Step 5: Take Λ → ∞.**
With counterterms in place, all S-matrix elements have finite Λ→∞ limits
when expressed in terms of m_R and e_R.

## Running Coupling

The physical coupling depends on the energy scale μ:
```
β(e) = μ ∂e_R/∂μ = e³/(12π²) + O(e⁵)    (QED)
```
e grows at high energy → Landau pole. In QCD (non-Abelian): β < 0 →
asymptotic freedom (coupling weakens at high energy).

## Renormalizability

A theory is "renormalizable" if ALL divergences can be absorbed into a
FINITE number of counterterms that have the same form as terms already
in the Lagrangian. This requires the coupling to have mass dimension ≥ 0.
QED (dim[e]=0) is renormalizable. Fermi's four-fermion theory (dim[G_F]=−2)
is NOT — new divergences appear at every order.

## Physical Meaning

The "bare" electron is surrounded by a cloud of virtual e⁺e⁻ pairs
(vacuum polarization) and photons. The physical electron is THIS
dressed object. The bare mass m₀ includes the self-energy of the cloud.
The "infinities" arise because we formulated the theory in terms of
bare particles that don't actually exist in isolation.

## Cross-References

- Landau Vol.4 §114-116 (radiative corrections, renormalization)
- Landau Vol.4 §127 (running coupling, asymptotic freedom in QCD)
- knowledge.qed.feynman_rules (diagrammatic foundation)
- reasoning.second_quantization (parent: the QFT framework)
- reasoning.small_parameter_expansion (pattern: expand in α = e²/ℏc ≈ 1/137)
