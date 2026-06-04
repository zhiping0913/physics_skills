---
skill_id: reasoning.em.magnetostatic_boundary_value
type: reasoning
summary_50t: >
  Current-free ∇×H=0 → H=−∇φ_m, ∇²φ_m=0 with BCs: φ_m continuous,
  μ∂φ_m/∂n continuous. Sphere: H_in=[3μ₀/(μ+2μ₀)]H₀, m=4πR³H₀(μ−μ₀)/(μ+2μ₀).
  Multi-region shielding. Duality E↔H, ε↔μ with electrostatics.
trigger:
  - magnetic material boundary-value problem in current-free region
  - magnetic sphere/shell in uniform applied B, shielding design
reasoning_role: magnetostatic_bvp
parent: reasoning.em.uniqueness_theorem_boundary_value
retrieval_cost: 1
---

# reasoning.em.magnetostatic_boundary_value — ∇×H=0 → Laplace BVP

## Core Picture

In current-free regions (∇×H = 0), introduce MAGNETIC SCALAR POTENTIAL φ_m:
H = −∇φ_m. With ∇·B = 0 and B = μH in linear media: ∇²φ_m = 0. The same
Laplace-equation, separation-of-variables, and multipole machinery as
electrostatics applies, with the duality substitutions E↔H, D↔B, ε↔μ.

## Derivation Sketch (from electrostatic BVP → magnetostatic analog)

Starting from `electrodynamics: reasoning.em.uniqueness_theorem_boundary_value`
(the uniqueness theorem guarantees a unique solution to ∇²φ_m = 0 given BCs):

1. **Existence of φ_m**: ∇×H = J_free = 0 in the region → H is irrotational →
   H = −∇φ_m (exact analog of E = −∇φ). In multiply-connected domains (toroidal
   coils), φ_m may be multi-valued; use winding numbers or switch to A.

2. **Laplace equation**: ∇·B = 0, B = μH in linear media → ∇·(−μ∇φ_m) = 0.
   For piecewise-constant μ: ∇²φ_m = 0 in each region.

3. **Boundary conditions at interface** (μ₁↔μ₂):
   - H_∥ continuous → φ_m,₁ = φ_m,₂ (up to an irrelevant additive constant)
   - B_⊥ continuous → μ₁ ∂φ_m,₁/∂n = μ₂ ∂φ_m,₂/∂n
   At infinity: φ_m → −H₀·r for uniform applied field H₀.

## Algorithm

```
1. In each region with uniform μ: solve ∇²φ_m = 0 via separation of variables
   (Legendre in spherical, Bessel in cylindrical).

2. General solution (spherical, azimuthally symmetric):
   φ_m(r,θ) = Σ [A_l r^l + B_l r^{-(l+1)}] P_l(cos θ)
   Far-field: A_l from applied H₀. Interior: B_l=0 at origin.

3. Apply BCs at each interface:
   - φ_m continuous → match coefficients
   - μ ∂φ_m/∂n continuous → match weighted radial derivatives
   → Solve the 2×2 (or N×N for multi-region) linear system.

4. Recover H from H = −∇φ_m, B = μH.
```

## Key Worked Examples

**Magnetic sphere** (radius R, permeability μ, in uniform H₀ along z):

```
φ_m,in(r,θ)  = −A r cos θ                     (A = 3μ₀/(μ+2μ₀) H₀)
φ_m,out(r,θ) = −H₀ r cos θ + m·r̂/(4πr²)      (dipole outside)

Inside: H_in = [3μ₀/(μ+2μ₀)] H₀     (UNIFORM, demagnetizing field)
        B_in = μ H_in = [3μ/(μ+2μ₀)] μ₀ H₀ = [3μ/(μ+2μ₀)] B₀
Outside: H_out = H₀ + dipole: m = 4πR³ [(μ−μ₀)/(μ+2μ₀)] H₀

Limits:
  μ→∞ (ideal ferromagnet): H_in→0, B_in→3μ₀H₀=3B₀, m=4πR³H₀
  μ→μ₀ (non-magnetic):     H_in→H₀, B_in→B₀, m→0 (field passes through)
  μ→∞, R→∞ (superconductor): H_in→0 (Meissner-like), m → perfect diamagnet
```

**Multi-region spherical shell shielding** (Jackson §5.12):

```
Regions: r<a (inner cavity, μ₀), a<r<b (shell, μ≫μ₀), r>b (outer, μ₀)
4 unknowns from 4 BCs at r=a and r=b.

For thin shell (t=b−a ≪ a) with μ ≫ μ₀:
  B_in/B₀ ≈ 9μμ₀b/(6μ²t) = 3μ₀b/(2μt)
  S = B₀/B_in ≈ 2μt/(3μ₀b)
  As μ→∞: B_in→0 (perfect shielding). As μ→μ₀: B_in→B₀ (no shielding). As a→b: B_in→B₀ (zero thickness).
Intuition: flux lines are sucked into the high-μ shell and shunted around
the inner cavity. Higher μ and thicker shell → better shielding.

For thick shell (general formula, Jackson §5.12 eq 5.120):
  Φ(ρ) = appropriate combination of r^l and r^{-(l+1)} terms matched at
  all interfaces. Need the l=1 term for uniform applied field.
```

## Electrostatics ↔ Magnetostatics Duality

| Electrostatics | Magnetostatics (∇×H=0) |
|---|---|
| E = −∇φ | H = −∇φ_m |
| D = εE | B = μH |
| ∇·D = ρ_f | ∇·B = 0 |
| ∇×E = 0 | ∇×H = J_f (=0 here) |
| ε | μ |
| φ continuous at interface | φ_m continuous |
| ε ∂φ/∂n continuous | μ ∂φ_m/∂n continuous |
| p = ∫ r ρ dV | m = ½∫ r×J dV (or m = V M for uniform M) |
| φ → −E₀·r at ∞ | φ_m → −H₀·r at ∞ |

## Edge Cases

- **Multiply-connected domains** (toroidal coil, current loop): ∇×H=0 holds
  locally but the line integral ∮ H·dl = NI ≠ 0 → φ_m is multi-valued. Use
  φ_m = φ_m₀ + (NI/2π)θ + winding numbers, or switch to vector potential A.
- **Permanent magnets**: ∇²φ_m = ∇·M (Poisson equation, not Laplace). The
  magnetization M acts as an effective magnetic charge density ρ_m = −∇·M
  in the volume and surface charge σ_m = M·n̂ on boundaries.
- **Nonlinear B-H** (hysteresis): iterative numerical solution needed;
  not covered by this linear template.

## Cross-References

- Jackson §5.9-5.12, Cao §2.69-2.78
- electrodynamics: reasoning.em.uniqueness_theorem_boundary_value (parent;
  same uniqueness theorem applies)
- electrodynamics: reasoning.em.helmholtz_decomposition (H = −∇φ_m + ∇×A
  for the general case; this node is the irrotational part)
- electrodynamics: knowledge.em.static_multipoles (multipole expansion
  → magnetic dipole moment m in the same framework)
- landau-graph: reasoning.equilibrium_as_extremum (energy minimum → Laplace)
