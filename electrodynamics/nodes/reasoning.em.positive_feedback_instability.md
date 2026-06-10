---
skill_id: reasoning.em.positive_feedback_instability
type: reasoning
summary_50t: >
  Positive-feedback instability skeleton: modulation δA → enhanced driving
  force δF ∝ δA → further growth of δA. Shared by wave collapse (δE → δn
  via ponderomotive → cavity → enhanced δE), relativistic self-focusing
  (δa₀ → δn via γ → lensing → enhanced δa₀), Kerr filamentation (δI →
  δn via n₂ → lensing → enhanced δI), and gravitational collapse (δρ →
  enhanced ∇²φ → enhanced compression). Mathematical structure: exponential
  growth Γ ∝ |A₀|², most unstable at k_opt ∼ (nonlinearity/diffraction)^{1/2}.
trigger:
  - recognizing when an instability is positive-feedback-driven vs parametric
  - computing collapse thresholds from nonlinearity vs dispersion balance
  - identifying the most unstable spatial scale
reasoning_role: positive_feedback_instability
parent: reasoning.em.nonlinear_optical_response
retrieval_cost: 1
sign_convention: >
  A₀ = pump amplitude. δA = perturbation. Γ = growth rate.
  k_opt = most unstable wavenumber. Nonlinearity coefficient α.
  Diffraction/dispersion coefficient β. Threshold: |A₀|² > |A_cr|².
---

# reasoning.em.positive_feedback_instability — δA → δF ∝ δA → Growth

## Core Picture

Many nonlinear systems exhibit collapse or explosive growth driven by the
same structural feedback loop: a perturbation δA modifies the medium in
a way that enhances the force driving δA, which further amplifies the
modification. This is distinct from parametric instability (where a pump
transfers energy to daughter waves via resonant 3-wave coupling). Here,
the PUMP IS THE MEDIUM: the perturbation modifies the pump's propagation,
which amplifies the perturbation. The canonical examples are wave collapse
in plasma (Zakharov 1972), relativistic self-focusing, Kerr filamentation,
and gravitational Jeans instability (Nonlinear Physics of Plasmas Ch.11,
Taflove FDTD §9.6).

## Derivation Sketch

### 1. The generic feedback loop

```
Step 1: Perturbation δA creates a medium response:
         δM = α |A₀| δA    [α = coupling coefficient]

Step 2: The modified medium alters the propagation of the pump A₀:
         (∂_t² − c₀²∇²) A₀ = −β δM A₀    [β = driving coefficient]

Step 3: The modified pump field enhances the perturbation:
         (∂_t² − c₀²∇²) δA = −β δM A₀    [same operator]

→ coupled equations: ∂_t² δA ∝ |A₀|² δA → exponential growth
```

For a transverse perturbation with wavenumber k_⟂:
```
Γ²(k_⟂) = α β |A₀|² k_⟂² − β₀ k_⟂⁴
```
where β₀ k_⟂⁴ represents diffraction/dispersion that stabilizes small scales.

### 2. Most unstable scale and threshold

```
∂Γ²/∂(k_⟂²) = 0 → k_opt² = (α β |A₀|²) / (2 β₀)

Γ_max = (α β |A₀|²) / (2√β₀)    [for k_opt]
```

The instability exists when Γ_max > 0, which is always true for any
|A₀|² > 0 in the local model. In practice, the threshold is set by
damping (ν) or system size (L):
```
|A₀|² > 2ν√β₀/(α β)    [damping-limited threshold]
k_opt L > 2π           [system-size threshold — at least one wavelength fits]
```

### 3. The "collapse" scenario

For systems where α β > 0 and there is no saturation mechanism:

**Phase 1 — Linear growth**: δA grows exponentially at Γ_max.
**Phase 2 — Nonlinear focusing**: δA becomes large → medium response δM
  saturates or changes sign → transition to self-similar collapse.
**Phase 3 — Singularity**: A → ∞ at a point in finite time (for cubic
  nonlinearity in 2D/3D). In physical systems, this is arrested by
  higher-order effects (wave breaking, ionization, viscosity).

### 4. Domain catalog

| Domain | A₀ (pump) | δM (medium mod.) | α | β | Saturation | Node |
|--------|----------|-----------------|---|---|-----------|------|
| **Langmuir collapse** | E_L (electric field) | δn_e/n₀ (density) | ponderomotive | ∇·(δn E) | Wave breaking | plasma |
| **Relativistic self-focusing** | a₀ (laser) | Δn(a₀) (index) | γ(a₀) mass | ∇²_⟂ N | Electron cavitation | lp.R9 |
| **Kerr filamentation** | E (optical) | Δn = n₂|E|² | χ⁽³⁾ | ∇²_⟂ N | Multiphoton ionization | uo.NLSE |
| **Ponderomotive self-focusing** | a₀ (laser) | δn_e(r) (density) | ∇|E|² | ∇²_⟂ N | Full electron expulsion | lp.R3 |
| **Jeans instability** | ρ₀ (density) | δφ (potential) | G (gravity) | ∇²φ = 4πGδρ | Pressure support | — |
| **Thermal self-focusing** | I (laser) | ΔT(I) → Δn | dn/dT | ∇²_⟂ N | Thermal diffusion | — |

All share the same Γ² ∝ |A₀|² k² − D k⁴ structure. Only α, β, and the
saturation mechanism differ.

### 5. Distinguishing from parametric instability

| Feature | Positive-feedback | Parametric (3-wave) |
|---------|-------------------|---------------------|
| Growth rate | Γ ∝ |A₀|² | γ₀ ∝ |A₀| |
| Daughter waves | None (self-modulation) | Two distinct modes (ω₁,k₁), (ω₂,k₂) |
| Transverse | Most unstable at finite k_⟂ | Resonant matching decides geometry |
| Saturation | Collapse or self-arrest | Pump depletion, wave breaking |
| Governing equation | NLS-type (4-wave) | Coupled-mode (3-wave) |

## Algorithm — Given (nonlinearity α, dispersion β₀, damping ν) → Instability

```
1. CHECK sign: α β must be positive for instability (self-focusing).
   If α β < 0: self-defocusing (stable).

2. MOST UNSTABLE SCALE:
   k_opt² = α β |A₀|² / (2 β₀).
   λ_opt = 2π/k_opt.

3. GROWTH RATE:
   Γ_max = α β |A₀|² / (2√β₀) [no damping].
   With damping: Γ = Γ_max − ν.

4. THRESHOLD: Γ > 0 → |A₀|² > 2ν√β₀/(α β).

5. CRITICAL POWER (for beam self-focusing):
   P_cr ∝ λ² β₀ / (α β n₀).
   P > P_cr → beam collapse.
```

## Edge Cases

- **Saturation vs collapse**: whether the feedback leads to a bounded
  equilibrium (self-trapping) or unbounded growth (collapse) depends on
  dimensionality and nonlinearity order. Cubic nonlinearity in 2D: critical
  collapse (threshold power). In 3D: supercritical (always collapses above P_cr).
- **Nonlocal response**: when the medium response δM extends beyond the
  perturbation size (e.g., thermal diffusion length > λ_opt), the instability
  is suppressed at small scales → larger λ_opt.
- **Competition with parametric instabilities**: at high pump power, both
  positive-feedback and parametric channels compete. The one with larger
  growth rate dominates. In laser-plasma: SRS (parametric) vs self-focusing
  (feedback) — the faster wins.

## Cross-References

- Nonlinear Physics of Plasmas (2010) Ch.11 — wave collapse
- Zakharov, JETP 1972 — Langmuir collapse theory
- Taflove FDTD (2005) §9.6 — nonlinear dispersive FDTD
- electrodynamics: reasoning.em.nonlinear_optical_response (parent — χ⁽³⁾ origin)
- laser-plasma: reasoning.lp.relativistic_self_focusing (R9 — plasma specialization)
- laser-plasma: reasoning.lp.ponderomotive_force (R3 — ponderomotive specialization)
- plasma: (future: wave_collapse — Langmuir specialization)
- ultrafast-optics: reasoning.uo.pulse_propagation_nlse_higher_order (Kerr specialization)
