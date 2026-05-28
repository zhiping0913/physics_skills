---
skill_id: knowledge.elasticity.hooke_law
type: knowledge
summary_50t: >
  σ_{ik} = K u_{ll} δ_{ik} + 2μ(u_{ik} − ⅓ u_{ll} δ_{ik}). K = λ+⅔μ (bulk modulus).
  μ (shear modulus). Young's modulus E = 9Kμ/(3K+μ). Poisson ratio ν.
  Navier equation: μ∇²u + (λ+μ)∇(div u) + f = 0.
trigger:
  - computing elastic deformations
  - stress-strain relations for isotropic solids
  - elastic waves, bending of beams and plates
reasoning_role: linear_elastic_response
parent: reasoning.elasticity_from_symmetry
retrieval_cost: 1
---

# knowledge.elasticity.hooke_law

**Hooke's law** (isotropic body):
```
σ_{ik} = λ u_{ll} δ_{ik} + 2μ u_{ik}
```
Separated into hydrostatic + shear:
σ_{ik} = K u_{ll} δ_{ik} + 2μ(u_{ik} − ⅓u_{ll}δ_{ik})
K = λ + ⅔μ (bulk modulus — resistance to volume change)
μ (shear modulus — resistance to shape change)

**Inverse**: u_{ik} = (1/9K) σ_{ll} δ_{ik} + (1/2μ)(σ_{ik} − ⅓σ_{ll}δ_{ik})

**Elastic constants relations**:
Young's modulus E = 9Kμ/(3K+μ). Poisson ratio ν = (3K−2μ)/(2(3K+μ)).
Range: −1 ≤ ν ≤ ½. Incompressible: ν→½ (K→∞).

**Navier equation** (static equilibrium):
μ∇²u + (λ+μ)∇(div u) + f = 0.
Elastic waves: c_l = √[(λ+2μ)/ρ] (longitudinal), c_t = √[μ/ρ] (transverse).

**Thermodynamic foundation** (§3-5):
dℰ = T dS + σ_{ik} du_{ik} (first law for elastic deformation).
F = F_0 + ½ λ u_{ii}² + μ u_{ik}² → σ_{ik} = ∂F/∂u_{ik}.

- Landau Vol.7 §1-8
