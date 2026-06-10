---
skill_id: reasoning.mt.soliton_formation
type: reasoning
summary_50t: >
  Soliton formation: balance of nonlinearity (wave steepening) and
  dispersion (wave spreading) producing stable localized wave packets.
  KdV soliton: u(x,t) = u₀ sech²((x−ct)/Δ), c = c₀ + u₀/3. NLS soliton:
  A(z,t) = A₀ sech(t/T₀) e^{iγP₀ z}. Shared by ion-acoustic solitons
  (plasma), optical solitons (fiber), Langmuir solitons (plasma), surface
  solitons, and BEC solitons. Domain distinction: which nonlinearity and
  which dispersion. Source: Nonlinear Physics of Plasmas Ch.6, Kivshar-
  Agrawal (Optical Solitons 2003).
trigger:
  - recognizing soliton formation conditions in any wave system
  - computing soliton width and amplitude from medium parameters
  - distinguishing KdV-type (weakly dispersive) vs NLS-type (strongly dispersive) solitons
reasoning_role: soliton_formation
parent: reasoning.em.nonlinear_optical_response
retrieval_cost: 1
sign_convention: >
  u(x,t) = wave field. c₀ = linear phase velocity. Δ = soliton width.
  Nonlinear coefficient α, dispersion coefficient β.
  KdV: u_t + α u u_x + β u_xxx = 0. NLS: iA_z − (β₂/2) A_tt + γ|A|²A = 0.
---

# reasoning.mt.soliton_formation — Balance of Nonlinearity and Dispersion

## Core Picture

A soliton is a self-reinforcing solitary wave that maintains its shape
while traveling at constant velocity. It arises from a precise BALANCE
between nonlinear wave steepening (which would form a shock) and
dispersion (which would spread the wave packet). This balance produces
a stable, localized structure that survives collisions with other solitons
— a property that emerges from the complete integrability of the underlying
PDE. Solitons appear across physics: water waves (Russell 1834), ion-acoustic
waves in plasma, optical pulses in fiber, Bose-Einstein condensates, and
magnetic domain walls. All share the same mathematical skeleton; only the
physical interpretation of the coefficients differs (Nonlinear Physics of
Plasmas Ch.6; Kivshar & Agrawal, Optical Solitons 2003).

## Derivation Sketch

### 1. The two canonical soliton equations

**Korteweg–de Vries (KdV)** — weakly dispersive, shallow-water-type:
```
u_t + α u u_x + β u_xxx = 0
```
Nonlinearity: α u u_x (steepening). Dispersion: β u_xxx (spreading).
Soliton solution: u(x,t) = u₀ sech²((x−ct)/Δ), c = c₀ + α u₀/3.

**Nonlinear Schrödinger (NLS)** — strongly dispersive, envelope-type:
```
i A_z − (β₂/2) A_tt + γ |A|² A = 0
```
Nonlinearity: γ |A|² A (self-phase modulation). Dispersion: β₂ A_tt (GVD).
Soliton solution: A(z,t) = √(P₀) sech(t/T₀) e^{iγP₀ z}.

### 2. Which equation emerges when?

The governing equation for a weakly nonlinear, weakly dispersive wave is:
```
u_t + c₀ u_x + α u u_x + β u_xxx + γ u_xxxxx + ... = 0
```
- **KdV regime**: when dispersion is WEAK (k Δx ≪ 1), the leading
  dispersive term is third-order (u_xxx). Nonlinearity and dispersion
  balance at the same order.
- **NLS regime**: when the wave is narrowband (Δω ≪ ω₀) and dispersion
  is STRONG at the carrier frequency, an envelope equation emerges via
  the slowly-varying envelope approximation (SVEA).
- **Boussinesq regime**: bidirectional propagation, retains both
  left- and right-going waves.

### 3. Soliton parameter relations

| Property | KdV soliton | NLS fundamental soliton |
|----------|------------|------------------------|
| Width Δ | √(12β/(α u₀)) | T₀ (free parameter) |
| Amplitude A₀ | u₀ | √(P₀) |
| Velocity c | c₀ + α u₀/3 | c₀ (carrier); envelope at v_g |
| A₀ × Δ² | 12β/α (constant) | P₀ T₀² = |β₂|/γ (N=1 condition) |
| Collision | Elastic (phase-shifted) | Elastic (phase-shifted) |
| Integrable? | Yes (IST solvable) | Yes (IST solvable) |

Key: for KdV, taller solitons are NARROWER and FASTER. For NLS, the
soliton order N² = γ P₀ T₀²/|β₂| determines the temporal profile.

### 4. Domain catalog

| Domain | Wave equation | u (field) | α (nonlin.) | β (disp.) | Soliton type | Node |
|--------|--------------|-----------|------------|----------|-------------|------|
| Ion-acoustic (plasma) | KdV | δn/n₀ | T_e/m_i | λ_D² ω_pi | KdV compres- sional | plasma |
| Langmuir (plasma) | NLS | E_L envelope | ω_p/n₀ T_e | 3 λ_D² ω_p | NLS envelope | plasma |
| Optical fiber | NLS | A(z,t) | n₂ ω₀/c A_eff | β₂ | NLS temporal | uo.NLSE |
| Shallow water | KdV | η(x,t) | 3c₀/2h₀ | c₀ h₀²/6 | KdV surface | — |
| BEC (Gross-Pitaevskii) | NLS | ψ(x,t) | g = 4πℏ²a_s/m | ℏ/(2m) | NLS matter-wave | — |
| Magnetic domain wall | sine-Gordon | φ(x,t) | sin φ | — | Topological | — |

### 5. Soliton stability — the role of integrability

A soliton is stable because the underlying PDE possesses an infinite set
of conserved quantities (Kruskal-Zabusky 1965). For KdV: mass ∫u dx,
momentum ∫u² dx, energy ∫(u³/3 − β u_x²) dx, and infinitely many higher
invariants. These conservation laws prevent the soliton from dispersing
or steepening into a shock — the two competing effects (nonlinearity and
dispersion) are locked into a dynamical equilibrium.

When integrability is broken (e.g., by damping, higher-order dispersion,
or inhomogeneity), solitons become "dissipative solitons" — they still
exist but require continuous energy input to maintain their shape.

### 6. The "soliton condition" across domains

For ANY wave system described by u_t + c₀ u_x + α u u_x + β u_xxx + ...:
```
SOLITON EXISTS when:  α β > 0   and   nonlinearity balances dispersion.
```
- α β > 0: nonlinearity and dispersion have the SAME sign → focusing.
- α β < 0: defocusing — no bright solitons (dark solitons or shocks instead).
- Balance condition: u₀ ∼ β/(α Δ²) for KdV, N² = γ P₀ T₀²/|β₂| = 1 for NLS.

## Algorithm — Given (wave system) → Soliton Parameters

```
1. IDENTIFY dominant nonlinearity (α) and dispersion (β) from the
   linearized dispersion relation and leading nonlinear term.

2. CHECK α β > 0. If not, bright solitons do not form.

3. KdV REGIME (weak dispersion):
   Δ = √(12β/(α u₀)), c = c₀ + α u₀/3.
   Soliton exists for any u₀ > 0 (but must satisfy weak-dispersion
   condition: Δ ≫ λ₀).

4. NLS REGIME (strong dispersion, narrowband):
   Fundamental soliton: P₀ T₀² = |β₂|/γ.
   Higher-order solitons: N² = γ P₀ T₀²/|β₂| = 4, 9, 16, ...

5. VERIFY: does the soliton width satisfy the assumptions?
   KdV: Δ ≫ λ₀ (weak dispersion). NLS: T₀ ≫ 1/ω₀ (SVEA).
```

## Edge Cases

- **Shock vs soliton**: when dispersion is negligible (β → 0), nonlinear
  steepening leads to wave breaking → shock formation. The soliton regime
  requires β to be large enough to arrest steepening before breaking.
- **Soliton-soliton collisions**: in integrable systems, two solitons pass
  through each other with only a phase shift. In near-integrable systems,
  collisions may produce small radiation.
- **Dimensionality**: KdV is 1D. In 2D/3D, transverse effects can destabilize
  solitons (e.g., transverse modulational instability of Langmuir solitons
  → wave collapse).

## Cross-References

- Nonlinear Physics of Plasmas (2010) Ch.6 — plasma solitons
- Kivshar & Agrawal, *Optical Solitons* (2003) — optical solitons
- Dauxois & Peyrard, *Physics of Solitons* (2006) — general soliton theory
- electrodynamics: reasoning.em.nonlinear_optical_response (parent — nonlinearity origin)
- ultrafast-optics: reasoning.uo.pulse_propagation_nlse (optical fiber specialization)
- plasma: (future: ion_acoustic_soliton, langmuir_soliton)
- electrodynamics: reasoning.em.positive_feedback_instability (sister node — collapse vs soliton)
