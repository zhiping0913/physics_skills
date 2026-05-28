---
skill_id: knowledge.quantum.wkb_approximation
type: knowledge
summary_50t: >
  Ψ ∝ (1/√p)exp(±i∫p dx/ℏ) (classical region). Ψ ∝ (1/√|p|)exp(−∫|p|dx/ℏ)
  (tunneling). Bohr-Sommerfeld: ∮p dq = (n+½)2πℏ. Connection at turning pts.
trigger:
  - semiclassical wave functions
  - quantization condition for 1D motion
  - tunneling probability through barrier
reasoning_role: semiclassical_method
parent: reasoning.wkb_quasiclassical
retrieval_cost: 1
---

# knowledge.quantum.wkb_approximation

**WKB wave function**: ψ ∝ (1/√p) exp(±(i/ℏ)∫p dx), p=√[2m(E−U)].

**Validity**: |dλ/dx| ≪ 1 with λ = 2πℏ/p. Equivalent: mℏ|F|/p³ ≪ 1.
FAILS at turning points (p→0) and for too-small momenta.

**Connection formulas** at turning point x=a (E=U(a)):
Left of turning point (classical): ψ = C·2/√p cos(∫_x^a p dx'/ℏ − π/4).
Right of turning point (forbidden): ψ = C·(1/√|p|)exp(−∫_a^x |p|dx'/ℏ).

**Bohr-Sommerfeld quantization**:
∮p dx = 2∫_{x₁}^{x₂} p dx = (n+½)·2πℏ, n=0,1,2,...
Equivalently: I = (n+½)ℏ where I = (1/2π)∮p dq (Vol.1 adiabatic invariant).

**Tunneling**: Transmission D = exp(−(2/ℏ)∫_{a}^{b}√[2m(U−E)] dx).
Exponential sensitivity to barrier width and height.

**3D**: ψ ∝ exp(iS₀/ℏ). S₀ satisfies H-J equation.
In central field: radial WKB + angular exact solution.

- Landau Vol.3 §46-53
