---
skill_id: reasoning.equilibrium_as_extremum
type: reasoning
summary_50t: >
  Physical equilibrium/ground state = extremum of a scalar functional
  (action, free energy, energy, entropy) over admissible configurations
  under constraints. Unifies least action, min F, max S, and variational QM.
trigger:
  - finding equilibrium/ground state of a physical system
  - system described by a functional whose extremum gives dynamics
  - need variational principle beyond classical mechanics (stat mech, QM, elasticity)
reasoning_role: variational_universal
parent: reasoning.variational_principle
children:
  - reasoning.classical_to_quantum_correspondence
  - reasoning.partition_to_thermodynamics
retrieval_cost: 1
---

# reasoning.equilibrium_as_extremum — Variational Principle Across All Physics

## Core Picture

The variational principle is not specific to classical mechanics. It is
the UNIVERSAL language of equilibrium physics. The form of the extremized
functional changes across domains, but the logic is identical:

```
Physical equilibrium = extremum of F[ψ] subject to constraints
```

The function F[ψ] encodes the physics. Finding the equilibrium means δF=0.

## The Universal Pattern

```
1. Identify the relevant functional F[ψ] for the setting.
2. Identify constraints (boundary conditions, conservation laws, normalization).
3. Apply δF[ψ] = 0. If constraints exist, use Lagrange multipliers.
4. The stationarity conditions ARE the equilibrium/dynamics equations.
```

## Instances Across All Physics

| Domain | Functional | Constraint | δF=0 gives |
|--------|-----------|------------|------------|
| Mechanics (V1) | Action S = ∫L dt | Fixed endpoints | Euler-Lagrange |
| Fields (V2) | Action S = ∫L d⁴x | Fixed boundary | Field equations |
| Stat mech (V5) | Entropy S = −Σ w_n ln w_n | ⟨E⟩,⟨N⟩ fixed | Gibbs distribution |
| Stat mech (V5) | Free energy F = E−TS | T,V fixed | Equilibrium state |
| Elasticity (V7) | ∫F(u_ik) dV | Boundary displacements | Navier-Cauchy eqns |
| QM (V3) | ⟨ψ|Ĥ|ψ⟩/⟨ψ|ψ⟩ | Normalization | Schrödinger eq (ground state) |
| Fluid (V6) | ∫(½ρv²+ρε) dV | Mass conservation | Steady flow eqns |

## The Same Mathematics, Different Names

In EVERY case, the condition δF = 0 leads to:
- **Euler-Lagrange** if F = ∫L(q,q̇,t) dt
- **Gibbs distribution** if F = entropy with ⟨E⟩ constraint
- **Rayleigh-Ritz** if F = ⟨ψ|Ĥ|ψ⟩ with ⟨ψ|ψ⟩=1
- **Navier-Cauchy** if F = elastic energy with boundary conditions

The agent should recognize: when a new volume introduces a new "principle"
(minimum free energy, maximum entropy, minimum elastic energy), it is
ALWAYS the same mathematical structure in different physical clothing.

## Landau Theory of Phase Transitions (Vol.5 §142-147)

This is the most important APPLICATION of the equilibrium-as-extremum
principle in statistical physics:

```
1. Identify the ORDER PARAMETER η that distinguishes the phases.
   (magnetization M, density difference ρ−ρ_c, etc.)
2. Near T_c, η is small → expand free energy:
   F(η) = F₀ + aη² + bη⁴ + ...  (odd terms vanish by symmetry)
3. Minimize: ∂F/∂η = 0 → η(2a + 4bη²) = 0
4. Second-order transition: a = a₀(T−T_c), b > 0.
   T > T_c: η = 0 (disordered). T < T_c: η = √[a₀(T_c−T)/2b].
5. Critical exponents (mean field): β = ½, γ = 1, δ = 3.
6. First-order if b < 0 or cubic term η³ present → discontinuous jump.
7. Ginzburg criterion (§146): fluctuations invalidate mean field when
   ⟨(Δη)²⟩/⟨η⟩² ∼ (T_c/T_c − T) ≠ small. Near T_c, need renormalization group.
```

**The reasoning IS the variational principle**: phase equilibrium = minimum
of F(η). All results (critical exponents, phase diagram, stability limits)
follow from expanding F to fourth order and minimizing.

## Non-Equilibrium Extension

The same logic extends to dynamics via δS=0 (least action). The
distinction is: equilibrium = extremum of a STATE functional;
dynamics = extremum of a PATH functional (action integral).

## Cross-References

- Landau Vol.1 §2 (least action)
- Landau Vol.3 §17, §20 (variational principle in QM, ground state energy)
- Landau Vol.5 §12, §15 (minimum free energy, maximum entropy)
- Landau Vol.7 §4-§5 (minimum elastic energy → equilibrium equations)
- reasoning.variational_principle (parent: classical least action)
- reasoning.partition_to_thermodynamics (instance: max S → Gibbs)
- reasoning.classical_to_quantum_correspondence (bridge: δ⟨Ĥ⟩=0 in QM)
