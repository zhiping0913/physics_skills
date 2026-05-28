---
skill_id: knowledge.em.energy_momentum_tensor_field
type: knowledge
summary_50t: >
  T^{ik} = (1/4π)(−F^{il}F^k_l + ¼g^{ik}F_{lm}F^{lm}).
  T^{00}=W (energy density), T^{0α}=S^α/c (Poynting vector).
  ∂T^{ik}/∂x^k = 0 for free field. From translation invariance of action.
trigger:
  - energy-momentum of EM field
  - conservation laws for field + matter
  - radiation pressure
reasoning_role: conserved_tensor
parent: knowledge.em.maxwell_from_action
retrieval_cost: 1
---

# knowledge.em.energy_momentum_tensor_field

**Energy-momentum tensor of EM field**:
```
T^{ik}_em = (1/4π)(−F^{il}F^k_l + ¼g^{ik}F_{lm}F^{lm})
```

**Components in 3D**:
```
T^{00} = (E²+H²)/8π = W              energy density
T^{0α} = S^α/c                        momentum density = Poynting/c
T^{αβ} = −σ_{αβ}                      Maxwell stress tensor
σ_{αβ} = (1/4π)[E_αE_β+H_αH_β − ½δ_{αβ}(E²+H²)]
```

**Conservation**: ∂T^{ik}/∂x^k = 0 in free space.
With charges: ∂T^{ik}_em/∂x^k = −(1/c)F^{ik}j_k (Lorentz force density).

**Virial theorem for EM field** (Vol.2 §34):
∫ T^α_α dV = 0 → ∫ (E²+H²)dV = 0 for static fields? No — T^μ_μ = 0
identically for EM (traceless). This has deep implications: the
energy-momentum tensor of EM is traceless → EM is scale-invariant
(classically).

- Landau Vol.2 §32-34
