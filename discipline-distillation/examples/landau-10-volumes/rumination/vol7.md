# Volume 7 Rumination Report — REDO

Date: 2026-05-26. Re-read §1-5, §7 with nodes loaded, compared line by line.

---

## 1. elasticity_from_symmetry — Several Gaps

### Missing: Nonlinear strain tensor
Landau §1 gives the FULL strain tensor:
u_{ik} = ½(∂u_i/∂x_k + ∂u_k/∂x_i + ∂u_l/∂x_i · ∂u_l/∂x_k)

The linearized version (dropping the last term) is an APPROXIMATION valid
only for small displacement gradients. Our template states only the
linearized form without mentioning that it's an approximation, or that
the full tensor is needed for large deformations (thin rods, plates).

### Missing: Why exactly TWO constants
Landau §4: "из компонент симметричного тензора u_{ik} можно составить
два независимых скаляра второй степени: u_{ii}² и u_{ik}²."

The counting argument is precise: from a symmetric 3×3 tensor, there
are exactly TWO independent quadratic scalar invariants. Isotropy reduces
the elastic constant tensor (21 components in general) to just 2.
Our template says "symmetry + isotropy → 2 constants" but doesn't explain
the scalar invariant argument.

### Missing: Shear/hydrostatic decomposition
Landau §4: "Всякую деформацию можно представить в виде суммы деформаций
чистого сдвига и всестороннего сжатия."

This separation is the physical reason K (bulk modulus) and μ (shear
modulus) are the NATURAL constants — they correspond to physically
distinct types of deformation. Our template's Algorithm mentions trace/
traceless but doesn't explain that this decomposition is the physical
origin of the two independent moduli.

### Missing: Thermodynamic foundation
Landau §3 establishes the thermodynamic identity dℰ = T dS + σ_{ik} du_{ik}
BEFORE deriving Hooke's law. The free energy expansion is thermodynamically
motivated, not just mathematically convenient. Our template presents the
free energy expansion as purely mathematical without mentioning the
thermodynamic origin.

### Missing: Isothermal vs adiabatic moduli
Landau §6 distinguishes isothermal (slow) and adiabatic (fast) elastic
constants. They differ: K_ad ≠ K, μ_ad = μ (shear modulus is the same!).
For most practical purposes the difference is small, but it's physically
important — sound waves involve adiabatic constants. Our template
doesn't mention this distinction at all.

### Missing: Stability conditions
Landau §4: K>0, μ>0 from requirement that free energy has MINIMUM at
undeformed state. This is the elastic analog of the thermodynamic
stability conditions. Our template mentions it in Algorithm step 5 but
doesn't explain the physical origin (minimum of free energy).

### Priority: All of the above

---

## 2. Summary

All fixes target the same node (elasticity_from_symmetry):

| # | Issue | Priority |
|---|-------|---------|
| 1 | Nonlinear vs linearized strain tensor | med |
| 2 | Why exactly 2 constants (scalar invariants) | high |
| 3 | Shear/hydrostatic physical decomposition | high |
| 4 | Thermodynamic foundation of free energy expansion | med |
| 5 | Isothermal vs adiabatic elastic moduli | med |
| 6 | Stability K>0, μ>0 from free energy minimum | low |

Total: 6 fixes. No new hidden parents.
