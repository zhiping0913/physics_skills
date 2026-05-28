---
skill_id: knowledge.em.lienard_wiechert
type: knowledge
summary_50t: >
  Potentials of an arbitrarily moving point charge. Construct 4-vector
  that reduces to Coulomb in rest frame: A^i = e u^i/(R_k u^k).
  φ = e/(R − v·R/c), A = ev/[c(R − v·R/c)]. All quantities at retarded time.
trigger:
  - field of a moving point charge
  - radiation from accelerated relativistic charges
  - relativistic plasma mirror (ROM) model foundation
reasoning_role: exact_solution_for_moving_charge
parent: knowledge.em.retarded_potentials
retrieval_cost: 1
---

# knowledge.em.lienard_wiechert

**Derivation logic** (Landau's elegant approach):
1. In rest frame of charge at retarded time t': φ = e/R, A = 0
2. Build 4-vector A^i that reduces to this: → A^i = e u^i/(R_k u^k)
3. R^k = (c(t−t'), r−r') is the null 4-vector from charge to observer
4. R_k R^k = 0 defines retarded time t' + R(t')/c = t

**3D form**:
```
φ = e / (R − v·R/c)             all at retarded time t'
A = ev / [c(R − v·R/c)]         R = r_obs − r_charge(t')
```

**Electric and magnetic fields** (Liènard-Wiechert → E, H):
```
E = e[(n−v/c)(1−v²/c²)/(κ³R²)]_ret + e[n×[(n−v/c)×v̇]]/(c²κ³R)_ret
H = [n×E]_ret
κ = 1 − n·v/c
```
First term: velocity field (∝1/R², quasi-static). Second term: acceleration
field (∝1/R, radiation).

**Key insight**: The denominator κ = 1 − n·v/c causes relativistic beaming.
When v→c, radiation is sharply peaked in the forward direction.

- Landau Vol.2 §63
