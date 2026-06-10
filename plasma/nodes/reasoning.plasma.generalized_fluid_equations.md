---
skill_id: reasoning.plasma.generalized_fluid_equations
type: reasoning
summary_50t: >
  Generalized fluid equation skeleton: ∂_t ρ + ∇·(ρv) = 0, ρ(∂_t + v·∇)v
  = −∇·P + F_ext + Q_correction. Shared by classical MHD, two-fluid plasma,
  quantum hydrodynamics (QHD, Bohm potential), and radiation hydrodynamics
  (radiation pressure). The correction term Q determines the physics regime:
  Q=0 → ideal MHD, Q=−(ℏ²/2m)∇(∇²√ρ/√ρ) → QHD, Q=∇·P_rad → radiation
  hydro. Source: Quantum Plasma (2025) Ch.5, Nonlinear Physics of Plasmas.
trigger:
  - recognizing which correction terms dominate in a given plasma regime
  - comparing QHD vs MHD predictions
  - understanding the mathematical hierarchy of fluid plasma models
reasoning_role: generalized_fluid_equations
parent: reasoning.plasma.mhd_equilibrium_stability
retrieval_cost: 1
sign_convention: >
  ρ = mass density. v = fluid velocity. P = pressure tensor.
  Q = correction term (force density). Bohm potential V_B = −(ℏ²/2m)
  (∇²√n/√n). P_rad = radiation pressure tensor. Classical MHD: Q=0.
---

# reasoning.plasma.generalized_fluid_equations — One Skeleton, Many Regimes

## Core Picture

Every fluid model of plasma — from ideal MHD to quantum hydrodynamics —
shares the same fundamental skeleton: continuity + momentum + energy.
The physics that distinguishes one regime from another enters as
CORRECTION TERMS to the pressure tensor and force density. Recognizing
this unified structure allows systematic reasoning: "Which term dominates?"
rather than "Which model should I use?" — a more physically grounded
approach (Quantum Plasma 2025 Ch.5, Nonlinear Physics of Plasmas).

## Derivation Sketch

### 1. The universal skeleton

For any plasma fluid description, the first two moments of the kinetic
equation (Vlasov, Wigner, or quantum kinetic) yield:

```
∂_t n + ∇·(n v) = 0                     [continuity — universal]
m n (∂_t + v·∇) v = −∇·P + q n (E + v×B) + Q    [momentum — skeleton]
```

where P is the pressure tensor and Q represents ALL physics beyond
the ideal Lorentz force. The energy equation (third moment) completes
the closure but follows the same pattern.

### 2. The pressure tensor hierarchy

| Closure | P (pressure tensor) | Validity |
|---------|---------------------|----------|
| **Cold fluid** | P = 0 | T ≪ T_F, T ≪ mc² |
| **Ideal MHD** | P = p I, p = n k_B T | Collisional, isotropic |
| **CGL (double adiabatic)** | P = diag(p_∥, p_⟂, p_⟂) | Collisionless, magnetized |
| **Full kinetic closure** | P_{ij} from Vlasov moment | General, requires distribution f(v) |
| **Fermi degenerate** | P_F = (3π²)^{2/3} (ℏ²/5m) n^{5/3} I | T ≪ T_F (quantum) |

### 3. The correction term Q — physics regime selector

```
Q = Q_ponderomotive + Q_quantum + Q_radiation + Q_collisional + Q_spin
```

**Q_ponderomotive** = −n ∇(e²|E|²/4m ω²)
— Dominant in laser-plasma interaction when a₀ > 0.1.
— Drives density cavitation, self-focusing, hole boring.

**Q_quantum (Bohm potential)** = n ∇(ℏ² ∇²√n / 2m² √n)
— Dominant when ℏ ω_p > k_B T (high density, low temperature).
— Provides "quantum pressure" that resists compression beyond the
  de Broglie wavelength scale.
— In QHD: replaces the classical pressure gradient in degenerate regimes.

**Q_radiation** = −∇·P_rad, where P_rad = (a T⁴/3) I in equilibrium
— Dominant when radiation energy density exceeds material energy density:
  a T⁴ > n k_B T → T > (n k_B / a)^{1/3}.
— Drives Marshak waves, radiation preheat in ICF.

**Q_collisional** = −ν n m (v_i − v_n) [ion-neutral friction, partially ionized]
— Dominant in weakly ionized plasmas (ν_in > ω_ci).

**Q_spin** = (μ_B/m) n ∇(s·B) [spin-magnetic coupling]
— Dominant in magnetized quantum plasmas where spin polarization is
  significant (μ_B B > k_B T).

### 4. The "which term dominates" diagnostic

For given plasma parameters (n, T, B, a₀, Z), compute the magnitude of
each Q term and compare:

| Term | Magnitude | Dominance condition |
|------|----------|-------------------|
| Pressure gradient | ∇p ∼ n k_B T / L | Always present (baseline) |
| Ponderomotive | n e² E₀² / (4 m ω² L) | a₀² > 4 k_B T / (m c²) (ω²/ω_p²) |
| Bohm (quantum) | n ℏ² / (m L³) | ℏ²/(m L²) > k_B T, or n > (m k_B T/ℏ²)^{3/2} |
| Radiation | a T⁴ / L | a T⁴ > n k_B T → T > (n k_B/a)^{1/3} |
| Lorentz (B) | q n v B | when ω_ce τ > 1 (magnetized) |

where L is the gradient scale length.

### 5. Regime diagram in (n, T) plane

```
T (eV)
  │
10⁶│  ┌──────────────┐
    │  │  Classical   │  Quantum
    │  │  (MHD,       │  (QHD,
10³│  │   two-fluid)  │   degenerate)
    │  ├──────────────┤
    │  │  Partially   │
 1  │  │  ionized     │
    │  └──────────────┘
    └────────────────────── n (cm⁻³)
     10¹⁵    10²⁰    10²⁵    10³⁰
```

Boundary: T ∼ T_F = (ℏ²/2m)(3π² n)^{2/3}.

### 6. Cross-domain fluid connections

The same skeleton appears beyond plasma physics:

| System | ρ | Force | Q (correction) |
|--------|---|-------|---------------|
| Neutral fluid (Navier-Stokes) | mass density | −∇p + η∇²v | Viscosity η |
| Superfluid (Gross-Pitaevskii) | |ψ|² | ∇p_q + Q_quantum | Quantum pressure |
| Dusty plasma | n_d (dust) | q_d (E + v×B) | Neutral drag |
| Radiation hydro | mass density | −∇(p + P_rad) | Radiative transfer |

All are instances of the same skeleton with different Q.

## Algorithm — Given (n, T, B, a₀) → Appropriate Fluid Model

```
1. COMPUTE T_F = (ℏ²/2m)(3π² n)^{2/3}.
   If T < T_F: quantum degeneracy → QHD needed (Q_quantum ≠ 0).

2. COMPUTE magnetization: ω_ce / ν_ei.
   If > 1: magnetized (Lorentz force important).
   If < 1: unmagnetized (scalar pressure suffices).

3. COMPUTE ponderomotive strength: a₀² vs 4 k_B T/(m c²)(ω²/ω_p²).
   If a₀² dominates: Q_ponderomotive must be included.

4. COMPUTE radiation pressure: aT⁴ vs n k_B T.
   If radiation dominates: add Q_radiation.

5. SELECT MODEL by dominant Q terms:
   Q=0 → ideal MHD.
   Q=Q_quantum → QHD.
   Q=Q_ponderomotive → laser-plasma envelope model.
   Q=Q_quantum+Q_ponderomotive → quantum laser-plasma.
```

## Edge Cases

- **Two-temperature fluids**: when T_e ≠ T_i (low collisionality), each
  species requires its own momentum equation. The skeleton scales to
  N species.
- **Non-ideal MHD**: Hall term (J×B/en) and electron pressure gradient
  in generalized Ohm's law. These are higher-order corrections to the
  single-fluid skeleton.
- **Kinetic effects**: when L ≤ λ_mfp (mean free path) or k λ_D > 0.3,
  the fluid closure fails and kinetic description is needed.

## Cross-References

- Quantum Plasma (2025) Ch.5 — QHD, DFT, QFT frameworks
- Nonlinear Physics of Plasmas (2010) Ch.3,9,11
- plasma: reasoning.plasma.mhd_equilibrium_stability (parent — MHD baseline)
- laser-plasma: reasoning.lp.ponderomotive_force (R3 — ponderomotive Q)
- laser-plasma: reasoning.lp.radiative_hydrodynamics (R16 — radiation Q)
