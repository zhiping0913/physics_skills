---
skill_id: convention.green_functions
type: convention
summary_50t: >
  Helmholtz: (∇²+k²)G = −δ(r−r') → G = e^{ikr}/(4πr). Poisson: ∇²G_P = −δ →
  G_P = 1/(4πr). Sommerfeld radiation condition (∂_r − ik)U → 0 selects outgoing.
  Jackson Gaussian uses −4πδ form — pure unit-system difference: G_Jackson = 4π G_project.
---

# Green's function normalization

## Helmholtz equation (project default, SI)

```
(∇² + k²) G(r, r') = −δ(r − r')   →   G(r, r') = e^{ik|r−r'|} / (4π |r−r'|)
```

The minus sign on the right is the project convention. It ensures that in the
static limit (k → 0), the Green's function reduces to the standard Poisson
Green's function with the same normalization.

**Sommerfeld radiation condition**:

```
lim_{r→∞} r (∂/∂r − ik) U(r) = 0
```

selects the **retarded** (outgoing) solution G ∼ e^{+ikr}/r. The advanced
solution G ∼ e^{−ikr}/r is never used except in formal derivations and is
immediately discarded.

For time-domain with e^{−iωt} convention, the retarded Green's function is:

```
G_ret(r, t; r', t') = δ(t' − t + |r−r'|/c) / (4π |r−r'|)     (time-domain Helmholtz-Green)
```

## Poisson equation (k → 0 limit)

```
∇² G_P(r, r') = −δ(r − r')   →   G_P(r, r') = 1 / (4π |r − r'|)
```

With SI Coulomb's law (∇²φ = −ρ/ε₀):

```
φ(r) = (1/ε₀) ∫ G_P(r, r') ρ(r') d³r' = (1/4πε₀) ∫ ρ(r')/|r−r'| d³r'
```

The 1/(4πε₀) of the Coulomb kernel is G_P/ε₀ in this convention; the 4π lives
in G_P, not as an extra factor in the field equation.

## Helmholtz-Kirchhoff theorem (project convention)

Using (∇²+k²)G = −δ (not −4πδ):

```
U(P) = ∮_S [ G ∂U/∂n − U ∂G/∂n ] dS
```

The factor of 1/(4π) is **inside** G. No additional prefactor appears.

This differs from Jackson §10.5 (Gaussian) where:

```
(∇² + k²) G_Jackson = −4π δ   →   G_Jackson = e^{ikr} / r
```

and the Helmholtz-Kirchhoff formula carries an explicit 1/(4π):

```
U(P) = (1/4π) ∮_S [ G_Jackson ∂U/∂n − U ∂G_Jackson/∂n ] dS
```

Both forms are **identical** in outcome. The conversion is:

```
G_Jackson = 4π × G_project
```

When substituting a Jackson Green's function into a project formula, drop the
explicit 1/(4π) and absorb it into G.

## How to apply in a cited formula

When a node cites a Jackson (SI edition) or Gaussian result involving a
Green's function:

1. **Identify** whether the source uses −δ or −4πδ on the RHS.
2. If −4πδ (Jackson Gaussian, Chew Gaussian-limit, Landau): multiply G by
   1/(4π) and drop any explicit 1/(4π) prefactor in integral formulas.
3. The final physical result (φ, E, U) must be unchanged — only the
   intermediate placement of the 4π differs.

## References

Jackson §6.4 (retarded G, SI), Jackson §10.5 (Helmholtz-Kirchhoff, Gaussian
convention), Chew §1.3 (radiation condition), Arfken §8.7 (Green's function
normalization conventions).
