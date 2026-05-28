---
skill_id: knowledge.em.maxwell_from_action
type: knowledge
summary_50t: >
  S = −Σmc∫ds − Σ(e/c)∫A_k dx^k − (1/16πc)∫F_ikF^{ik}dΩ.
  Varying A_i → ∂F^{ik}/∂x^k = −(4π/c)j^i (Maxwell with sources).
  ∂_i F_{kl} + ∂_k F_{li} + ∂_l F_{ik} = 0 (Bianchi — automatic from F=∂A−∂A^T).
trigger:
  - need Maxwell equations from first principles
  - coupling EM field to charges
reasoning_role: field_equations_from_action
parent: reasoning.action_decomposition_field_theory
retrieval_cost: 1
---

# knowledge.em.maxwell_from_action

**Total action**: S = S_m + S_mf + S_f
```
S_m = −Σ mc∫ ds                   free particles
S_mf = −Σ (e/c)∫ A_k dx^k         interaction
S_f = −(1/16πc)∫ F_ik F^{ik} dΩ  EM field
```

**4D Maxwell equations**:
```
∂F^{ik}/∂x^k = −(4π/c) j^i        (fields with sources)
∂_i F_{kl} + ∂_k F_{li} + ∂_l F_{ik} = 0  (homogeneous — from F=∂A−∂A^T)
```

**3D form**:
```
div E = 4πρ                      ∇×E = −(1/c)∂B/∂t
∇×B = (4π/c)j + (1/c)∂E/∂t      div B = 0
```

**Conservation**: ∂j^i/∂x^i = 0 → ∂ρ/∂t + div j = 0 (charge conservation
is a consequence of Maxwell equations + antisymmetry of F_ik).

**Energy density**: W = (E²+H²)/8π
**Poynting vector**: S = (c/4π)[E×H]
**Energy conservation**: ∂W/∂t + div S = −j·E

- Landau Vol.2 §26-31
