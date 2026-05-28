---
skill_id: reasoning.elasticity_from_symmetry
type: reasoning
summary_50t: >
  Strain: u_{ik} = ½(∂u_i/∂x_k + ∂u_k/∂x_i). Hooke: σ_{ik} = λu_{ll}δ_{ik} + 2μu_{ik}.
  Same constitutive pattern as viscous stress (Vol.6). Symmetry + isotropy
  → 2 elastic constants. Free energy expansion → unique linear stress-strain.
trigger:
  - modeling elastic deformations
  - need stress-strain relation for isotropic solid
  - seeking analogies between continuum theories
reasoning_role: constitutive_linear_response
parent: reasoning.constitutive_relation_from_symmetry
children:
  - knowledge.elasticity.hooke_law
retrieval_cost: 1
---

# reasoning.elasticity_from_symmetry — Small Deformations → Linear Elasticity

## Core Picture

A solid under small deformation returns to its original shape —
this is elasticity. The displacement field u_i(r) = x_i' − x_i describes
how each point moves. The strain tensor u_{ik} (FULL nonlinear form):
u_{ik} = ½(∂u_i/∂x_k + ∂u_k/∂x_i + ∂u_l/∂x_i · ∂u_l/∂x_k).
For small displacement gradients, the last term is neglected →
u_{ik} = ½(∂u_i/∂x_k + ∂u_k/∂x_i) (linearized strain).

**Why exactly two elastic constants**: A symmetric 3×3 tensor u_{ik}
has exactly TWO independent quadratic scalar invariants: u_{ii}² (trace
squared) and u_{ik}² (sum of squares). Isotropy + scalarity of free energy
→ F = F₀ + ½λ u_{ii}² + μ u_{ik}². This counting argument replaces the
general 21-component elastic constant tensor with just λ, μ.

**Shear vs hydrostatic decomposition**: Every deformation decomposes
into PURE SHEAR (shape change, no volume change) + HYDROSTATIC COMPRESSION
(volume change, no shape change):
u_{ik} = (u_{ik} − ⅓δ_{ik}u_{ll}) + ⅓δ_{ik}u_{ll}.
In the alternative form: F = μ(u_{ik} − ⅓δ_{ik}u_{ll})² + ½K u_{ll}²,
K = λ + ⅔μ is the BULK modulus and μ is the SHEAR modulus — each controls
a physically distinct mode of deformation.

**Isothermal vs adiabatic** (§6): K_ad ≠ K but μ_ad = μ. Shear modulus
is the same for slow and fast deformations. Sound waves involve ADIABATIC
constants. Usually E Tα²/C_p ≪ 1, so difference is small.

## Algorithm

```
1. Define displacement field: u_i(r) = x_i' − x_i
2. Strain tensor (linearized): u_{ik} = ½(∂u_i/∂x_k + ∂u_k/∂x_i)
3. Thermodynamic foundation (§3): dℰ = T dS + σ_{ik} du_{ik}
   → Free energy: dF = −S dT + σ_{ik} du_{ik}
4. Stress from force balance: ∂σ_{ik}/∂x_k + ρg_i = 0
5. Free energy expansion (two scalar invariants):
   F = F₀ + ½ λ u_{ii}² + μ u_{ik}²
   Alternative: F = μ(u_{ik}−⅓δ_{ik}u_{ll})² + ½K u_{ll}², K = λ + ⅔μ
6. Hooke's law: σ_{ik} = ∂F/∂u_{ik} = λ u_{ll} δ_{ik} + 2μ u_{ik}
   = K u_{ll} δ_{ik} + 2μ(u_{ik} − ⅓δ_{ik} u_{ll})
7. Stability: K > 0, μ > 0 (F has minimum at undeformed state)
```

## The Analogies (Landau's Hallmark)

| Elasticity | Fluid (Vol.6) | Electrostatics (Vol.8) |
|-----------|---------------|----------------------|
| u_{ik} (strain) | ∂v_i/∂x_k (velocity gradient) | — |
| σ_{ik} (stress) | σ'_{ik} (viscous stress) | — |
| div σ + f = 0 | ρ(∂v/∂t+v·∇v) = div σ + f | — |
| Lamé eqns = Navier eqn | Navier-Stokes | Poisson eqn ∇²φ = −4πρ |

## Cross-References
- Landau Vol.7 §1-5
- Landau Vol.6 §15 (viscous stress — same symmetry reasoning!)
- Landau Vol.8 §6-7 (dielectric polarization — same free energy expansion logic)
