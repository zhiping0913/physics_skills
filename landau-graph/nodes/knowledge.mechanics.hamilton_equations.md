---
skill_id: knowledge.mechanics.hamilton_equations
type: knowledge
summary_50t: >
  H = Σ pᵢq̇ᵢ − L. q̇ᵢ = ∂H/∂pᵢ, ṗᵢ = −∂H/∂qᵢ.
  For any f(q,p,t): df/dt = {f,H} + ∂f/∂t.
trigger:
  - switching to Hamiltonian form
  - using phase space methods
reasoning_role: phase_space_formalism
parent: reasoning.canonical_transformation
children:
  - knowledge.mechanics.poisson_brackets
  - knowledge.mechanics.hamilton_jacobi_equation
retrieval_cost: 1
---

# knowledge.mechanics.hamilton_equations

**Definition**: H(q,p,t) = Σ pᵢq̇ᵢ − L, with q̇ expressed via p.

**Canonical equations**:
```
q̇ᵢ = ∂H/∂pᵢ,   ṗᵢ = −∂H/∂qᵢ
```
2s first-order ODEs instead of s second-order.

**Energy connection**: H = E if L = T − U and T quadratic in q̇.
H ≠ E if L has linear velocity terms or ∂L/∂t ≠ 0.

**Phase space volume conservation** (Liouville): ∮dqdp is a canonical invariant.
→ foundation of statistical mechanics.

**Poisson brackets**: {f,g} = Σ (∂f/∂qᵢ ∂g/∂pᵢ − ∂f/∂pᵢ ∂g/∂qᵢ)
→ {f,H} = df/dt.  {qᵢ,pⱼ} = δᵢⱼ, {qᵢ,qⱼ} = {pᵢ,pⱼ} = 0.

- Landau Vol.1 §40-42, §46
