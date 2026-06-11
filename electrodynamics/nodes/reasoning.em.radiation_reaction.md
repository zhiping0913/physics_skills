---
skill_id: reasoning.em.radiation_reaction
type: reasoning
summary_50t: >
  Abraham-Lorentz-Dirac equation: m du^μ/dτ = F_ext^μ + (2e²/3c³)
  [d²u^μ/dτ² + u^μ(du^ν/dτ)(du_ν/dτ)/c²]. Runaway solutions pre-accelerate.
  Landau-Lifshitz reduction: replace a^μ with F_ext^μ/m to first order.
  Classical self-energy renormalization: observed mass = bare + δm_em.
trigger:
  - radiation back-reaction on relativistic electron motion
  - laser-plasma electron dynamics at extreme intensity (a₀ > 100)
reasoning_role: radiation_reaction
parent: reasoning.em.lienard_wiechert_radiation
retrieval_cost: 1
---

# reasoning.em.radiation_reaction — Self-Force on Accelerated Charge

## Core Picture

An accelerating charge radiates. The radiation carries away energy and momentum,
which must react back on the charge. The radiation-reaction force is the
classical self-force — the field produced by the charge AT ITS OWN POSITION,
acting back on itself. This is the Abraham-Lorentz-Dirac (ALD) equation:

```
m a = F_ext + (2e²/3c³) \dot{a}    [non-relativistic ALD]
```

The \dot{a} term (jerk) generates PATHOLOGICAL pre-acceleration: the charge
begins accelerating BEFORE the external force acts (runaway solutions).

## Derivation Sketch

### 1. Non-relativistic Abraham-Lorentz force

The self-force is the net momentum lost to radiation, balanced by force:
```
F_rad · v = −P_rad = −(μ₀ e²/6πc) a²
```
Integrating by parts over a periodic motion (or assuming negligible boundary
terms — the key idealization): ∫ F_rad·v dt = (μ₀ e²/6πc) ∫ \dot{a}·v dt. This gives:
```
F_rad = (μ₀ e²/6πc) \dot{a} = (2e²/3c³) \dot{a}
```

### 2. Relativistic ALD (Dirac 1938)

The covariant generalization uses the radiation-green's function self-field:
```
m₀ du^μ/dτ = F_ext^μ + (2e²/3c³)[d²u^μ/dτ² + u^μ (du^ν/dτ)(du_ν/dτ)/c²]
```
The second term in brackets (proportional to u^μ) ensures the orthogonality
condition u_μ F_rad^μ = 0 (4-velocity ⊥ 4-acceleration in proper time).

### 3. The runaway problem

The homogeneous ALD equation m a = τ \dot{a} (τ = 2e²/3mc³ ≈ 6×10⁻²⁴ s)
has the general solution: a(t) = a₀ exp(t/τ) — exponential growth on the
timescale τ. This is the RUNAWAY SOLUTION: the charge spontaneously
accelerates to c with no external force. Physically unacceptable.

### 4. Landau-Lifshitz reduction (LL 1962)

The LL procedure eliminates runaways by iterative reduction: replace \dot{a}
in ALD with its lowest-order expression from the Lorentz force:
```
F_rad^μ ≈ (2e²/3mc³)[(q/m)∂_ν F_ext^{μν} u_ν + (q²/m²) F_ext^{μν} F_ext_{νλ} u^λ
         − (q²/m²c²)(F_ext_{λν} u^ν)(F_ext^{λκ} u_κ) u^μ]
```
This is a SECOND-ORDER differential equation (no runaways) that is accurate
to order (τ/T)² where T is the external field timescale.

### 5. Regime of applicability

The LL equation is valid when the radiation-reaction force is small compared
to the Lorentz force — i.e., in the CLASSICAL regime ℏω ≪ m c² (no pair
production). For laser-plasma: the quantum parameter χ determines the
boundary: χ = (eℏ/m³c⁴)|F_μν u^ν| ∼ a₀ (ℏω/mc²). When χ ∼ 1, quantum
effects (pair production, discrete photon emission) dominate.

## Algorithm — Given (electron trajectory, external field) → radiation-corrected motion

```
1. Compute classical Larmor power P = (μ₀ e² a²/6πc) × γ⁶ correction.
2. Check: is P × (pulse duration) ≪ γ m c²? → radiation reaction negligible.
3. If not negligible: solve Landau-Lifshitz equation (NOT ALD — no runaways).
4. Monitor diag: is dE_rad/dt < F_ext·v? → LL valid.
5. Check quantum parameter χ = γ |F_perp|/E_Sch (E_Sch = m²c³/eℏ).
6. If χ > 0.1: classical LL breaks down → QED-PIC needed.
```

## Edge Cases

- **Laser-electron collision at extreme a₀**: for a₀ > 100 at optical
  wavelength, χ ∼ 1 and classical radiation reaction gives only the
  continuous limit of quantum stochastic photon emission.
- **Dirac's asymptotic condition**: the only physically acceptable solution
  to ALD satisfies a(τ) → 0 as τ → ∞ (no runaways). This gives the
  integro-differential form with advanced Green's function — equivalent
  to the LL reduction.

## Cross-References

- Jackson §16, Griffiths §11.2, Lechner Ch.16
- landau-graph: knowledge.em.lienard_wiechert (retarded fields)
- electrodynamics: reasoning.em.lienard_wiechert_radiation (radiation from acceleration)
- laser-plasma: reasoning.lp.radiation_reaction (quantum corrections, pair production)
