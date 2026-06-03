---
skill_id: reasoning.plasma.mhd_equilibrium_stability
type: reasoning
summary_50t: >
  Ideal MHD: J×B=∇p equilibrium. Energy principle: δW>0→stable. Safety
  factor q(r)=rB_φ/RB_θ. Kruskal-Shafranov: q>1. Ballooning, kink,
  interchange. β limit: Troyon β_N<3.5. Tearing: resistive, Δ'>0.
trigger:
  - analyzing MHD equilibrium and stability of toroidal/linear plasma
  - computing stability boundaries for fusion devices
reasoning_role: mhd_stability
parent: reasoning.equilibrium_as_extremum
retrieval_cost: 1
references:
  - landau-graph: reasoning.equilibrium_as_extremum (δW minimization)
---

# reasoning.plasma.mhd_equilibrium_stability — J×B=∇p → Stability

## Core Picture

Ideal MHD describes plasma as a conducting fluid. Equilibrium: J×B = ∇p
(force balance). Stability: small displacement ξ(r) must NOT lower potential
energy — δW(ξ) > 0 for all ξ.

## Derivation Sketch (from equilibrium extremum → MHD stability)

Starting from `landau-graph: reasoning.equilibrium_as_extremum` (which
establishes that stable equilibria minimize potential energy), the MHD
energy principle is the plasma-specific realization:

1. **From variational principle to δW**: the ideal MHD Lagrangian
   L = ∫ d³x [ρ v²/2 − B²/2μ₀ − p/(γ−1)] yields, upon linearization
   with displacement ξ(r,t) = ξ(r)e^{−iωt}, the quadratic form
   δW = −(1/2) ∫ ξ·F(ξ) d³x where F is the self-adjoint force operator.
   KEY INSIGHT: F is Hermitian → ω² is PURELY REAL in ideal MHD;
   instability manifests as ω² < 0 (exponential growth), not complex ω.

2. **Grad-Shafranov equation** (axisymmetric equilibrium): taking
   curl of J×B=∇p with axisymmetry (∂/∂φ=0) yields the GS equation:
   Δ*ψ = −μ₀R² dp/dψ − F dF/dψ
   where ψ is the poloidal flux, Δ* = R² ∇·(R^{−2} ∇) the elliptic
   operator, p(ψ) and F(ψ)=RB_φ are free functions (profiles).
   KEY NON-OBVIOUS: the GS equation is a nonlinear elliptic PDE;
   the choice of p(ψ) and F(ψ) determines the equilibrium shape.

3. **Solovév solution** (analytical GS): for p'(ψ) = const and
   FF'(ψ) = const (linear profiles), the GS equation has the exact
   solution ψ = ψ₀ + (R²−R₀²)²/8 + (Z²(R²+R₀²) + Z⁴/2)/4 (in
   cylindrical R,Z coordinates). This gives up-down symmetric D-shaped
   equilibria. The **Shafranov shift** Δ(r) is the outward displacement
   of flux surfaces due to toroidicity — proportional to β_p + l_i/2.

4. **Hall MHD and two-fluid corrections**: at small scales (d_i = c/ω_pi),
   the generalized Ohm's law E + v×B = ηJ + (1/ne)(J×B − ∇p_e) adds
   the Hall term J×B and electron pressure gradient. This breaks the
   frozen-in condition for electrons (field lines slip relative to
   electron fluid while frozen to ion fluid). Modifies tearing mode
   physics (collisionless reconnection at d_i scale) and introduces
   whistler-wave dynamics into MHD.

5. **Stellarator equilibrium**: without axisymmetry, equilibrium is
   inherently 3D. The magnetic field is B = ∇Φ (vacuum) + non-axisymmetric
   components from external coils. No continuous symmetry → no GS equation;
   instead solve ∇p = J×B in 3D with nested flux surfaces constrained
   by coil geometry. Existence of flux surfaces is not guaranteed —
   islands and stochastic regions appear at low-order rational surfaces.
   Modern optimization (NESCOIL, STELLOPT) shapes the boundary and coils
   to maximize flux-surface quality and minimize neoclassical transport.

## Equilibrium (Friedberg §4, Chen §6)

**Grad-Shafranov equation** (axisymmetric toroidal):
Δ*ψ = −μ₀R² dp/dψ − F dF/dψ
where ψ(R,Z) is the poloidal flux function.

**Solovév solution** (analytic GS for linear profiles): p'(ψ)=const,
FF'(ψ)=const → ψ(R,Z) gives up-down symmetric D-shape. Shafranov shift
Δ(r) = (R(r) − R₀)/a ∝ β_p + l_i/2 measures the outward displacement of
the magnetic axis due to toroidal pressure (hoop force + tire-tube force).

**Safety factor** (tokamak): q(r) = r B_φ / R B_θ.
Rational surface: q = m/n where field lines close after m toroidal, n poloidal turns.

**Beta**: β = 2μ₀⟨p⟩/B₀². Troyon limit: β_N = β a B₀/I_p < 3.5.

## Energy Principle (Friedberg §8)

```
δW = (1/2)∫ dV [ |Q|²/μ₀ + γp|∇·ξ|² + (ξ·∇p)(κ·ξ)
                  − 2(ξ_⊥·∇p)(ξ·κ) − J_∥ (ξ_⊥×n)·Q_⊥ ]
where Q = ∇×(ξ×B₀), κ = (b·∇)b (field line curvature).
```

δW < 0 for ANY ξ → unstable. Terms: |Q|² (field-line bending, stabilizing),
γp|∇·ξ|² (compression, stabilizing), pressure + curvature (destabilizing
if ∇p·κ > 0: bad curvature), parallel current (kink drive).

## Major Instabilities

| Mode | n | Condition | Consequence |
|------|---|-----------|-------------|
| Kink (external) | 1 | q(a) < 1 | Disruption |
| Kink (internal) | 1 | q(0) < 1 | Sawtooth crash |
| Interchange/flute | ∞ | ∇p·∇B > 0 (bad curvature) | Pressure limit |
| Ballooning | ∞ | β > β_crit | Localized at outboard |
| Tearing (resistive) | >0 | Δ' > 0 | Magnetic islands |
| RWM (resistive wall) | 1 | β > β_no-wall | Wall-stabilized |

## Edge Cases

- **X-point and separatrix geometry**: the GS equation is singular at
  X-points (B_pol = 0). Equilibrium solvers must handle the separatrix
  carefully — flux surfaces are no longer nested beyond it. The X-point
  region introduces a diverted plasma with scrape-off layer (SOL).
  Stability analysis breaks down when field lines are open — energy
  principle must include sheath boundary conditions at divertor plates.
  Use extended MHD (two-fluid) or SOL transport codes (SOLPS).
- **β → β_crit (ballooning limit)**: ballooning modes localize to the
  outboard midplane where curvature is destabilizing. The ballooning
  equation (Fourier transform along field line in the high-n limit)
  is an ODE: d/dθ [g(θ) dξ/dθ] + [α h(θ) − λ] ξ = 0, where α = −q²R dp/dr
  is the ballooning parameter. Stability boundary: α_crit(Mercier, ŝ).
  When ballooning-stable but β close to limit, the energy principle
  eigenfunction becomes EXTREMELY localized → WKB breakdown; use the
  ballooning formalism (Connor-Hastie-Taylor) with full periodicity.
- **Stellarator equilibrium → no axisymmetry**: the GS equation does not
  apply. Equilibrium is a 3D free-boundary problem solved iteratively
  (VMEC for fixed boundary, NSTAB for stability). Flux surfaces may not
  exist globally (island chains, ergodic regions). Use 3D MHD codes
  (VMEC + TERPSICHORE/COBRA) for equilibrium; stability is mode-family
  dependent (N-periodic). When large islands form at low-order rational
  surfaces, the nested-flux-surface assumption breaks down — use
  PIES/HINT for island equilibria or RMHD.
- **Hall MHD / two-fluid regime**: when L ∼ d_i (ion skin depth), the
  frozen-in condition for electrons is broken. The generalized Ohm's law
  E + v×B = ηJ + (d_i/L)(J×B − ∇p_e)/ne introduces dispersive whistler
  waves and enables fast collisionless reconnection. The ideal-MHD energy
  principle is no longer self-adjoint (ω² complex). Use extended MHD
  or full two-fluid when d_i is resolvable. Breaks down when electron
  inertia scale d_e = c/ω_pe is reached — further corrections needed.
- **Tearing mode at small Δ'**: Δ' < 0 is linearly stable in slab, but
  in toroidal geometry, neoclassical effects (bootstrap current perturbation)
  can drive the NTM unstable even when Δ' < 0. The modified Rutherford
  equation includes Δ'_GGJ + bootstrap + curvature terms. Use neoclassical
  tearing mode (NTM) theory when bootstrap is significant.

## Cross-References

- Friedberg §4-9, Chen §6
- landau-graph: reasoning.equilibrium_as_extremum (energy principle)
- landau-graph: reasoning.physical_solution_selection (stable ↔ δW>0)
