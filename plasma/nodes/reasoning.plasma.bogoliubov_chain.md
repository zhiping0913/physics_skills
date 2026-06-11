---
skill_id: reasoning.plasma.bogoliubov_chain
type: reasoning
summary_50t: >
  Liouville → BBGKY: ∂f_s/∂t + {H_s, f_s} = ∫ ∂V/∂q · ∂f_{s+1}/∂p. Bogoliubov
  functional hypothesis: f_s(t) = F_s[f₁(t)] for t ≫ τ_c. Closure at s=2 →
  Landau collision integral: ∂f₁/∂t = ∫ d³p₂ dσ |v₁−v₂| (f₁'f₂' − f₁f₂).
trigger:
  - deriving kinetic equation from first principles
  - understanding the microscopic origin of the Landau collision operator
reasoning_role: bogoliubov_chain
parent: knowledge.kinetic.boltzmann_equation
retrieval_cost: 1
---

# reasoning.plasma.bogoliubov_chain — N-Particle → 1-Particle via BBGKY

## Core Picture

The microscopic dynamics of N ~ 10²³ particles is governed by the reversible
Liouville equation for the N-particle distribution f_N. The kinetic equation
for the one-particle distribution f₁ is obtained by systematic reduction through
the BBGKY hierarchy (Bogoliubov–Born–Green–Kirkwood–Yvon), with Bogoliubov's
functional hypothesis providing the CLOSURE that introduces irreversibility.
This is the fundamental derivation of the Landau collision integral — it does
NOT come from a phenomenological ansatz but from the N-body Liouville equation.
(Voprosy Vol.1, Silin §; Landau Vol.10, Ch.1).

## Derivation Sketch

### 1. From Liouville to BBGKY

The N-particle distribution f_N(Γ, t) satisfies the Liouville equation
∂f_N/∂t + {H, f_N} = 0. Defining the reduced s-particle distribution:

```
f_s(q₁...q_s, p₁...p_s, t) = V^s ∫ f_N dΓ_{N-s}
```

and integrating the Liouville equation over (N−s) particles yields the
BBGKY hierarchy:

```
∂f_s/∂t + {H_s, f_s} = (N−s)/V ∫ d³r_{s+1} d³p_{s+1} ∂V_{i,s+1}/∂r_i · ∂f_{s+1}/∂p_i
```

Each equation for f_s couples to f_{s+1} — an INFINITE chain, as inescapable
as the moment hierarchy (see `reasoning.plasma.generalized_fluid_equations`).

### 2. Bogoliubov's functional hypothesis (the crucial closure)

Bogoliubov (1946) proposed that after a short initial transient t ∼ τ_c
(collision time), ALL higher-order distributions become functionals of
the one-particle distribution:

```
f_s(t) = F_s[f₁(t)]    for t ≫ τ_c
```

This is the hypothesis of the "kinetic stage" — the system "forgets" its
initial correlations and the entire statistical state is enslaved to f₁.
The functional F_s is then expanded in powers of the plasma parameter
g = 1/(n λ_D³) ≪ 1 (weak coupling):

```
f₂(1,2) = f₁(1) f₁(2) + g g₂(1,2) + O(g²)
```

where g₂ captures the pair correlations. Substituting into the BBGKY
equation for s=1 and truncating at O(g²) yields the LANDAU KINETIC EQUATION.

### 3. Emergence of the Landau collision integral

For a spatially uniform plasma, the kinetic equation for species a colliding
with species b reduces to:

```
∂f_a/∂t = −(2π q_a² q_b² lnΛ/m_a) ∂/∂v_i ∫ d³v' U_{ij}(u)
          [f_a(v) ∂f_b(v')/∂v'_j − f_b(v') ∂f_a(v)/∂v_j]
```

where u = v − v', U_{ij}(u) = (u²δ_{ij} − u_i u_j)/u³ is the Coulomb
collision tensor, and lnΛ = ∫_{b_min}^{b_max} db/b = ln(λ_D/ρ_min) is the
Coulomb logarithm — the accumulated effect of all impact parameters from
the Landau length ρ_min = e²/(4π ε₀ k_B T) to the Debye length λ_D.

The Landau form is a Fokker-Planck equation in velocity space with the
diffusion tensor D_{ij} and friction vector F_i emerging from the same
integral kernel — the Einstein relation between diffusion and friction
is automatically satisfied.

### 4. The three stages of relaxation

Bogoliubov's analysis reveals three well-separated timescales:
```
τ_c ≪ τ_relax ≪ τ_hydro
```
- **Kinetic stage** (t ∼ τ_c): binary correlations build up, Bogoliubov's
  functional synchronisation to f₁ completes.
- **Relaxation stage** (t ∼ τ_relax = τ_c/g): f₁ evolves via the Landau
  equation toward local Maxwellian f_M(n, v̄, T). Total entropy increases.
- **Hydrodynamic stage** (t ≫ τ_relax): the macroscopic parameters n(r,t),
  v̄(r,t), T(r,t) evolve on the slow diffusive timescale — described by
  the Navier-Stokes/Braginskii equations.

After the hydrodynamic stage, the system locally satisfies f₁ = f_M everywhere:
the full Bogoliubov chain has collapsed to five moments (ρ, v, T).

## Cross-References

- Bogoliubov, *Problems of Dynamical Theory in Statistical Physics* (1946)
- Landau Vol.10, Ch.1 (BBGKY → Landau integral)
- Voprosy Teorii Plazmy Vol.1 (1963), Silin §: Coulomb collision derivation
- landau-graph: knowledge.kinetic.boltzmann_equation (parent)
- landau-graph: knowledge.kinetic.landau_collision_integral (end product)
- plasma: reasoning.plasma.generalized_fluid_equations (same closure logic in fluid hierarchy)
