---
skill_id: reasoning.plasma.dispersion_relation_method
type: reasoning
summary_50t: >
  Linearize fluid/Vlasov + Maxwell → N×(N×E)+ε·E=0 → det=0 → D(k,ω)=0.
  Electrostatic (ε_l=0) vs electromagnetic (N²=ε). Phase/group velocity,
  accessibility, cutoffs (k→0) and resonances (k→∞). Universal plasma wave algorithm.
trigger:
  - finding wave modes in any plasma model (cold, warm, kinetic, MHD)
  - computing ω(k) or k(ω) from linearized equations
reasoning_role: dispersion_method
parent: reasoning.normal_mode_decomposition
retrieval_cost: 1
references:
  - landau-graph: reasoning.normal_mode_decomposition (same eigenvalue structure)
  - electrodynamics: reasoning.em.waveguide_mode_decomposition (same math)
---

# reasoning.plasma.dispersion_relation_method — Linearize → D(k,ω)=0

## Core Picture

Finding plasma waves always follows the same algorithm, regardless of the
plasma model (cold fluid, warm fluid, kinetic Vlasov, MHD):

```
Linearized equations → plane wave ansatz → eliminate variables → det = 0
```

The result is the DISPERSION RELATION D(k,ω)=0, which encodes everything:
propagating vs evanescent, phase/group velocity, damping/growth, cutoffs/resonances.

## Algorithm (Stix §1, Chen §4, Ginzburg §1)

```
1. CHOOSE MODEL: cold fluid (n, v, E, B), warm fluid (+ p), or kinetic (f₀(v)).
2. LINEARIZE: n=n₀+ñ, v=ṽ, E=Ẽ, B=B₀+B̃. Drop ñ·ṽ, ṽ×B̃, etc.
3. FOURIER: all perturbations ∝ exp[i(k·r − ωt)].
4. ELIMINATE: express ñ, ṽ, B̃ in terms of Ẽ using continuity, momentum, Maxwell.
5. WAVE EQUATION: N×(N×Ẽ) + ε·Ẽ = 0  where N = ck/ω.
   (Same form in Gaussian and SI after ε conversion; load
   `si-gaussian-conversion` when reading Stix or Ginzburg.)
6. DETERMINANT: det|N_i N_k − N²δ_ik + ε_ik| = 0 → D(k,ω) = 0.
7. SOLVE: ω(k) [initial value] or k(ω) [boundary value].
```

## Classification by Polarization

**Electrostatic (ES)**: E∥k, B̃=0. Condition: ε_l(k,ω) ≡ k̂·ε·k̂ = 0.
Examples: Langmuir waves (ω²=ω_p²+3k²v_th²), ion acoustic, Bernstein.

**Electromagnetic (EM)**: E⊥k, B̃≠0. Condition from full wave equation.
Further split by angle to B₀: ∥ (R/L), ⊥ (O/X), oblique.

## Cutoffs and Resonances

- **Cutoff**: N→0 (k→0). Wave reflected. Condition: a term in D vanishes.
  Accessibility: wave can only propagate where N²>0 (between cutoffs).
- **Resonance**: N→∞ (k→∞). Wave absorbed or mode-converted.
  Condition: coefficient of N⁴ vanishes. Example: ω=ω_ce (R-wave), S=0 (X-mode).

## Cross-References

- Stix §1-2, Chen §4, Ginzburg §1-2
- landau-graph: reasoning.normal_mode_decomposition (same eigenvalue logic)
- electrodynamics: reasoning.em.waveguide_mode_decomposition (same mathematical structure)
