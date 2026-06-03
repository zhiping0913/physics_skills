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

## Equilibrium (Friedberg §4, Chen §6)

**Grad-Shafranov equation** (axisymmetric toroidal):
Δ*ψ = −μ₀R² dp/dψ − F dF/dψ
where ψ(R,Z) is the poloidal flux function.

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

## Cross-References

- Friedberg §4-9, Chen §6
- landau-graph: reasoning.equilibrium_as_extremum (energy principle)
- landau-graph: reasoning.physical_solution_selection (stable ↔ δW>0)
