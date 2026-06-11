---
skill_id: reasoning.plasma.instability_classification
type: reasoning
summary_50t: >
  Free energy source determines instability type. Configuration-space (fluid):
  ∇n, ∇T, ∇B, J → MHD instabilities (δW<0). Velocity-space (kinetic):
  non-Maxwellian f₀ → inverse Landau (∂f₀/∂v>0). Penrose criterion for
  absolute vs convective. Threshold and growth rate from D(k,ω)=0.
trigger:
  - plasma is observed to be unstable, need to identify mechanism
  - computing instability threshold and growth rate
reasoning_role: instability_taxonomy
parent: knowledge.kinetic.plasma_instabilities
retrieval_cost: 1
references:
  - landau-graph: knowledge.kinetic.plasma_instabilities
---

# reasoning.plasma.instability_classification — Free Energy → Growth

## Core Picture

All plasma instabilities draw free energy from either CONFIGURATION space
(gradients in real space) or VELOCITY space (non-Maxwellian distributions).

## Derivation Sketch — From D(k,ω)=0 to Growth Rate

Starting from `landau-graph: knowledge.kinetic.plasma_instabilities` (which
provides the dispersion relation D(k,ω)=0 for unstable modes), the taxonomy
of instabilities follows the SOURCE of free energy:

### Phase 0: The universal instability derivation algorithm

1. **Choose equilibrium** (f₀, B₀, n₀(r), T₀(r)) and perturbation (ñ, ṽ, Ẽ, B̃).
2. **Linearize** Vlasov+Maxwell or fluid equations around equilibrium.
3. **Fourier transform** → D(k,ω)=0 via `plasma: reasoning.plasma.dispersion_relation_method`.
4. **Solve** ω(k) = ω_r + iγ; instability ⇔ γ=Im ω > 0.
5. **Identify free-energy source** — which equilibrium gradient (∂n₀/∂r, ∂T₀/∂r,
   ∂f₀/∂v > 0, J×B) drives the instability. This last step IS the classification.

### Phase 1: Two fundamental routes to Im ω > 0: The dispersion relation D(k,ω)≡0
   defines ω(k). Writing D = D_R + i D_I, and expanding for small Im ω:
   ```γ = Im ω ≈ −D_I / (∂D_R/∂ω)```
   Instability (γ>0) requires D_I and ∂D_R/∂ω to have opposite signs.
   D_I comes from EITHER: fluid terms (∇n, ∇T, ∇B, J — configuration space)
   OR kinetic terms (resonant particles with ∂f₀/∂v > 0 — velocity space).

2. **Penrose criterion** (kinetic, 1D electrostatic): for a distribution f₀(v),
   stability requires: ∫^{∞}_{−∞} dv (f₀(v) − f₀(v_min)) / (v − v_min)² < 1
   where v_min is the velocity at the minimum of f₀. Equivalent: the number of
   "bumps" in f₀ determines stability. Procedure: (a) find all extrema of f₀(v);
   (b) at each local minimum v₀, evaluate the Penrose integral; (c) if ANY
   integral exceeds 1, the distribution is unstable to a mode with phase
   velocity near v₀. The Nyquist method (complex ω-plane contour integration
   of D(k,ω)) gives the same result — count encirclements of the origin.

3. **MHD energy principle** (configuration-space): δW = δW_F + δW_S + δW_V
   with fluid, surface, and vacuum contributions. The Suydam criterion
   (local interchange in cylindrical pinch): r B_z²/8 (q'/q)² + dp/dr > 0.
   Mercier criterion generalizes to toroidal geometry. Newcomb's method
   solves the marginal-stability Euler-Lagrange equation for ξ(r) — the
   number of zero-crossings of ξ determines the number of unstable modes
   (Sturm-Liouville oscillation theorem). Δ' for tearing: the jump in the
   logarithmic derivative of the perturbed flux across the rational surface;
   Δ' > 0 → tearing unstable, Δ' < 0 → stable.

4. **Connecting the two classes**: some instabilities have hybrid free-energy
   sources. Drift waves: ∇n₀ provides the configuration-space drive, but
   electron Landau resonance determines the sign of γ. Two-stream (beam):
   kinetic at low density (Landau resonance), reactive/fluid at high density
   (wave coupling, no resonant particles).

## Two Fundamental Classes

### Configuration-Space (Fluid/MHD) Instabilities

Free energy source: spatial gradients.

| Instability | Free energy | Condition | Example |
|------------|-------------|-----------|---------|
| Rayleigh-Taylor | ∇p opposite to g | Heavy fluid on top of light | Pellet ablation |
| Kelvin-Helmholtz | Velocity shear | v₁≠v₂ at interface | Magnetopause |
| Interchange/flute | ∇p·∇B < 0 (bad curvature) | δW < 0 | Tokamak edge, mirror |
| Kink (m=1) | Parallel current | q(a) < 1 (Kruskal-Shafranov) | Tokamak disruption |
| Sausage (m=0) | Azimuthal current | Any k, pinch | Z-pinch |
| Tearing | ∇J (current gradient) | Δ' > 0 | Island formation, sawteeth |
| Drift wave | ∇n₀ | Universal (always unstable) | Tokamak turbulence |

**Method**: Ideal MHD energy principle: δW < 0 ↔ unstable.
Full expression: see `knowledge.plasma.mhd_waves_stability`.
Configuration-space instabilities are classified by the free-energy
source term in δW (pressure gradient, current, curvature).

**Diagnostic tests for δW**:
- **Suydam criterion** (cylindrical, local): satisfies rB_z²/8 (q'/q)² + p' > 0 for stability. Fails near rational surfaces when pressure gradient is steep.
- **Mercier criterion** (toroidal generalization of Suydam): includes toroidal coupling and shear. Used for internal (m≥2) modes.
- **Newcomb's method**: solve the marginal (γ=0) Euler-Lagrange equation for ξ(r) around a rational surface. Count zero-crossings of ξ — each crossing corresponds to one unstable mode (Sturm-Liouville theorem). Provides exact stability boundaries for 1D cylindrical equilibria.
- **Δ' (tearing parameter)**: compute the jump [ψ'/ψ] across the rational surface r_s from the outer ideal-MHD solution. Δ' > 0 → tearing unstable; Δ' = 0 → marginal; Δ' < 0 → stable. Δ' is independent of resistivity but the growth rate γ ∝ η^{3/5} (Δ')^{4/5} for constant-ψ tearing.

### Velocity-Space (Kinetic) Instabilities

Free energy source: ∂f₀/∂v > 0 somewhere.

| Instability | f₀ feature | Waves | Damping |
|------------|-----------|-------|---------|
| Bump-on-tail | ∂f₀/∂v > 0 at v_bump | Langmuir | Inverse Landau |
| Loss-cone | ∂f₀/∂v_⊥ > 0 | Whistler, ECM | Cyclotron maser |
| Temperature anisotropy | T_⊥ > T_∥ | Whistler, EMIC | Anisotropy-driven |
| Beam (two-stream) | Two cold beams | Electrostatic | Reactive (fluid) |
| Ion acoustic (current) | v_dr > c_s (electron drift) | Ion acoustic | Ion Landau competes |

**Method**: Penrose criterion — ∫ dv (∂f₀/∂v)/(v − ω/k) determines stability.
Nyquist analysis of D(k,ω) in complex ω-plane.

**Penrose procedure step-by-step** (1D electrostatic):
1. Compute f₀(v). Find all local minima and maxima.
2. For each local minimum at v=v₀, evaluate I(v₀) = ∫ dv [f₀(v)−f₀(v₀)]/(v−v₀)².
3. If any I(v₀) > 1, the distribution is Penrose-unstable. The unstable ω/k lies near v₀.
4. For multi-species, sum contributions: I_total = Σ (ω_pα²/k²) I_α.
5. Equivalent Nyquist criterion: plot D_R(ω_r) vs D_I(ω_r) for ω_r from −∞ to ∞; if the contour encircles the origin (for D(k,ω) with ω on the real axis and Im ω → −∞ below), there are unstable roots.

## Absolute vs Convective

- **Absolute** (ω complex, k real): grows in time at fixed position.
- **Convective** (ω real, k complex): grows in space, advected away.
- Determined by Green's function response to impulse (Briggs-Bers criterion).

## Edge Cases

- **δW > 0 but unstable resistively**: ideal MHD predicts stability, but
  finite resistivity enables tearing modes (Δ'>0). The ideal-MHD energy
  principle is necessary but not sufficient for resistive stability.
  Use resistive MHD (tearing Δ') or two-fluid when η≠0.
- **Stable ∂f₀/∂v < 0 everywhere but still unstable**: the Penrose criterion
  applies to 1D electrostatic only. In magnetized plasma, instabilities
  can arise from anisotropy (T_⊥/T_∥ drivers) even when ∂f₀/∂v∥ < 0
  everywhere. Use the full electromagnetic kinetic dispersion with the
  Bessel-function expansion — the firehose and mirror instability conditions
  (β_∥−β_⊥ > 2 and β_⊥(T_⊥/T_∥−1) > 1, respectively) capture this.
- **Threshold regime (γ → 0⁺)**: near marginal stability, linear theory
  predicts exponential growth but nonlinear saturation may quench it before
  observable amplitude is reached. The linear threshold is a necessary
  condition; use nonlinear saturation estimates (quasilinear flattening,
  mode coupling) to determine whether the instability MATTERS.
- **Multi-mode competition**: real plasmas are never unstable to just ONE
  mode. The fastest-growing linear mode may not dominate nonlinearly —
  use the Manheimer or Dimits shift concept: zonal flows and other secondary
  modes can suppress the primary instability.

## Cross-References

- Chen §6-7, Stix §10, Friedberg §8-9
- landau-graph: knowledge.kinetic.plasma_instabilities (kinetic types)
- landau-graph: reasoning.physical_solution_selection (Penrose ↔ causality)
