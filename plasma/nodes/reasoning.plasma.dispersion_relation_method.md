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

## Derivation Sketch (from normal-mode decomposition → plasma D(k,ω))

Starting from `landau-graph: reasoning.normal_mode_decomposition` (which
establishes that any linear PDE system can be decomposed into eigenmodes
via det=0), the plasma-specific dispatch follows:

1. **Model-dependent ε(k,ω) feeds the universal wave equation**:
   N×(N×E) + ε·E = 0. The same determinant structure applies whether
   ε is cold fluid, warm fluid, or kinetic — only the functional form of
   ε_ij(k,ω) changes. KEY INSIGHT: the algorithm (linearize → Fourier →
   eliminate → det=0) is MODEL-AGNOSTIC.

2. **Landau prescription for causality**: in kinetic theory, the velocity-space
   integral ∫ dv f₀(v)/(ω−kv) is singular on the real ω-axis. The correct
   analytic continuation (Landau 1946) replaces ω → ω+i0⁺, moving the pole
   BELOW the integration contour. This yields the plasma dispersion function
   Z(ζ) = π^{−1/2} ∫^{∞}_{−∞} dt e^{−t²}/(t−ζ), with Im ζ > 0, analytically
   continued to Im ζ ≤ 0 (Stix §8). The imaginary part Im[Z(ζ)] ∝ exp(−ζ²)
   encodes collisionless (Landau) damping — obtained directly from the det=0
   prescription, no collisions needed.

3. **Bers-Briggs pinch-point analysis** (absolute vs convective): when D(k,ω)=0
   has complex ω AND complex k, the nature of the instability is determined by
   the Green's function response to a localized impulse. Compute ω(k) for
   complex k; if the integration contour for the inverse Laplace-Fourier
   transform is PINCHED between two roots of D(k,ω)=0 merging from opposite
   half-planes as Im ω → −∞, the instability is ABSOLUTE (grows in place).
   Otherwise it's CONVECTIVE (advected away). The pinch-point (k₀,ω₀) satisfies
   D(k₀,ω₀)=0 AND ∂D/∂k|_{k₀}=0. This is the rigorous criterion; the heuristic
   "Im ω > 0 for real k → absolute" is only sufficient, not necessary.

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

## MHD Reduction from Two-Fluid

Algorithm (Chen §3, Friedberg §1-2):
1. Start from two-fluid momentum: m_e n_e dV_e/dt = −∇p_e − en_e(E + V_e×B) − m_e n_e ν_ei(V_e−V_i); same for ions.
2. Add → single-fluid: ρ dV/dt = J×B − ∇p (ideal MHD limit).
3. Subtract → generalized Ohm's law: E + V×B = ηJ + (1/en_e)(J×B − ∇p_e) + (m_e/e²n_e)∂J/∂t.
4. Ordering analysis for different MHD regimes (table):
   - Ideal MHD: η→0, Hall term negligible, electron inertia negligible → E + V×B = 0
   - Resistive MHD: keep ηJ term → flux diffusion, reconnection
   - Hall MHD: keep (1/ne)J×B → whistler, fast reconnection
   - Electron MHD: keep ∂J/∂t → collisionless skin depth
5. Cross-ref: `plasma: reasoning.plasma.mhd_equilibrium_stability`, `knowledge.plasma.mhd_waves_stability`.

## Edge Cases

- **k → 0 (spatially uniform)**: D(k,ω) reduces to a pure algebraic condition
  on ω. The "wave" becomes a global oscillation (e.g., plasma oscillation at
  ω=ω_p). Dispersion-relation methods still work; the eigenfrequency is found
  from ε(ω)=0. Breaks down when boundary effects are important — use full
  boundary-value problem (Poisson + sheath) instead.
- **|k| → ∞ (small wavelength)**: N² → ∞. In cold plasma, resonances produce
  this limit. The fluid model breaks down when kλ_D ∼ 1 or kρ_L ∼ 1 — use
  kinetic dispersion with Z(ζ) function and full Bessel expansion.
- **ω-complex vs k-complex ambiguity**: the same D(k,ω)=0 can be solved for
  ω(k) with k real (temporal growth) or k(ω) with ω real (spatial growth).
  These give DIFFERENT predictions for convective systems. The Bers-Briggs
  pinch-point analysis (Derivation Sketch §3) resolves which is physical —
  don't just pick the easier math.
- **Multiple roots coalescing (mode conversion)**: when two branches of D(k,ω)=0
  approach each other, the WKB approximation breaks down. Use full-wave
  integration or Budden tunnelling theory (Stix §18). The cold-plasma equation
  AN⁴ − BN² + C = 0 has a mode-conversion point where the two N² solutions
  coincide (B² − 4AC = 0).
- **Electrostatic approximation fails**: ε_l=0 only decouples from EM when
  k is exactly parallel or perpendicular to B₀. For oblique propagation,
  the ES and EM branches are coupled — the full determinant must be used,
  not the simplified ε_l=0 condition. When in doubt, compute the full det
  and check if |E⊥|/|E∥| is small.

## Cross-References

- Stix §1-2, Chen §4, Ginzburg §1-2
- landau-graph: reasoning.normal_mode_decomposition (same eigenvalue logic)
- electrodynamics: reasoning.em.waveguide_mode_decomposition (same mathematical structure)
