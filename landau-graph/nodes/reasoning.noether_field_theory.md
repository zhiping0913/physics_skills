---
skill_id: reasoning.noether_field_theory
type: reasoning
summary_50t: >
  Continuous symmetry of field action → conserved Noether current ∂_μ j^μ = 0.
  Translation invariance → energy-momentum tensor T^{μν}. U(1) → charge current.
  The field-theoretic generalization of Vol.1 symmetry_to_conservation.
trigger:
  - constructing conserved currents from field action symmetries
  - deriving T^{ik} for EM, elastic, or fluid fields
  - need to understand where the energy-momentum tensor COMES FROM
reasoning_role: noether_field
parent: reasoning.symmetry_drives_physics
children:
  - knowledge.em.energy_momentum_tensor_field
  - reasoning.lorentz_invariance_to_action
retrieval_cost: 1
---

# reasoning.noether_field_theory — Field Symmetry → Conserved Current

## Core Picture

The Noether theorem generalizes from point mechanics (Vol.1) to fields:
every continuous symmetry of the field action S = ∫L(φ, ∂_μ φ) d⁴x
produces a conserved current ∂_μ j^μ = 0. The conserved CHARGE
Q = ∫ j⁰ d³x is the field-theoretic analog of the conserved quantity
in point mechanics.

This is the bridge from Vol.1 symmetry_to_conservation to ALL field
theories in Vol.2, Vol.6, Vol.7, and Vol.8. Without it, T^{ik} and
other field-theoretic conserved quantities appear as memorized formulas.

## Algorithm: From Symmetry to Conserved Current

**Step 1: Write the field action.**
S = ∫ L(φ_A, ∂_μ φ_A) d⁴x, where φ_A are all fields (A indexes them).

**Step 2: Identify the continuous symmetry.**
Infinitesimal transformation: x^μ → x^μ + δx^μ, φ_A → φ_A + δφ_A.
For spacetime translations: δx^μ = ε^μ, δφ_A = 0 (for scalar fields).

**Step 3: Compute the CHANGE in the Lagrangian density.**
Under the transformation, L changes by δL. Compute this explicitly.

**Step 4: Use the equations of motion.**
∂L/∂φ_A = ∂_μ(∂L/∂(∂_μ φ_A)). This is the Euler-Lagrange equation for fields.

**Step 5: Rearrange into a total divergence.**
The result takes the form: ∂_μ j^{μ} = 0, where j^{μ} is the Noether current.

## Energy-Momentum Tensor from Translation Invariance

The most important special case: translation invariance x^μ → x^μ + ε^μ.

```
δL = ε^ν ∂_ν L (L changes because its argument x changes)
   = ∂_μ [T^{μν} ε_ν] where T^{μν} is the canonical energy-momentum tensor

Canonical form: T^{μν} = ∂L/∂(∂_μ φ) · ∂^ν φ − g^{μν} L
```

**For the EM field** (L = −(1/16π)F_{μν}F^{μν}):
T^{μν} = (1/4π)[F^{μλ}F^ν_λ + (1/4)g^{μν}F_{λσ}F^{λσ}]

**Belinfante symmetrization**: The canonical T^{μν} is generally NOT
symmetric. For a gauge-invariant theory, adding ∂_λ B^{λμν} (with
B antisymmetric in λ,μ) produces a symmetric T^{μν}_{sym} without
changing the conservation law or total energy-momentum.

## Instances: Same Algorithm, Different Fields

| Theory | Action L | Symmetry | Conserved current |
|--------|---------|----------|-------------------|
| EM (V2) | −F²/16π | Translation | T^{ik} = (F^{iλ}F^k_λ + δ^{ik}F²/4)/4π |
| Scalar field | ½∂_μ φ ∂^μ φ | Translation | T^{μν} = ∂^μ φ ∂^ν φ − g^{μν}L |
| Dirac field (V4) | ψ̄(iγ^μ∂_μ − m)ψ | U(1) gauge | j^μ = ψ̄γ^μ ψ (charge current) |
| Fluid (V6) | (see Vol.6 §7) | Translation | Π_{ik} = ρv_i v_k + pδ_{ik} − σ'_{ik} |
| Elasticity (V7) | ½λu_{ii}² + μu_{ik}² | Translation | σ_{ik} = ∂F/∂u_{ik} |

## The Bridge to Point Mechanics

The Noether current j^{μ} for a symmetry integrates to a conserved charge:
Q = ∫ j⁰ d³x, dQ/dt = 0.

For translation invariance: Q = P^ν = ∫ T^{0ν} d³x is the 4-momentum.
This is the field-theoretic analog of P = Σ m_a v_a from Vol.1.

## Cross-References

- Landau Vol.2 §29, §32 (EM energy-momentum tensor)
- Landau Vol.4 §10 (Dirac charge current from U(1))
- Landau Vol.6 §7 (momentum flux tensor)
- Landau Vol.7 §2 (stress tensor from elastic energy)
- reasoning.symmetry_to_conservation (point mechanics parent)
- reasoning.symmetry_drives_physics (pattern parent)
